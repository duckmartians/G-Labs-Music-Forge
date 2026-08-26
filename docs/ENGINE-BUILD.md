# Đóng gói Python engine cho bản release

Backend Node spawn engine theo thứ tự ưu tiên (backend/core/engine.js):

1. `MLAB_ENGINE` env (đường dẫn executable) — để test bản đóng gói.
2. `resources/bin/engine/mlab-engine(.exe)` — bản PyInstaller trong app release.
3. `engine/.venv/bin/python -m mlab_engine` — dev mode (venv trong repo).

Dev không cần làm gì thêm ngoài tạo venv:

```bash
cd engine
python3.12 -m venv .venv
./.venv/bin/pip install demucs onnxruntime librosa soundfile music21 pretty_midi numpy scipy resampy typing_extensions mir_eval
./.venv/bin/pip install --no-deps basic-pitch
```

> basic-pitch phải cài `--no-deps`: bản pip của nó pin tensorflow-macos cũ
> không có wheel cho Python ≥3.12. Thiếu TF thì basic-pitch tự chọn backend
> ONNX (onnxruntime đã cài ở trên) — đã verify chạy tốt.

## Build engine binary (khi làm bản release)

PyInstaller **onedir** (onefile giải nén mỗi lần chạy → chậm và to):

```bash
cd engine
./.venv/bin/pip install pyinstaller
./.venv/bin/pyinstaller --noconfirm --onedir --name mlab-engine \
  --collect-all demucs --collect-all basic_pitch --collect-all librosa \
  --collect-all music21 --collect-data pretty_midi \
  --hidden-import mlab_engine \
  --paths . -c entry.py
# entry.py: from mlab_engine.__main__ import main; import sys; sys.exit(main())
```

Kết quả `engine/dist/mlab-engine/` copy vào:

- macOS: `bin/engine/mac/` (electron-builder map → `resources/bin/engine`)
- Windows: `bin\engine\win\` (build trên máy Windows, giống quy tắc exe của
  Video Downloader — không cross-build)

Lưu ý dung lượng: torch chiếm phần lớn (~vài trăm MB mỗi nền tảng). Model
htdemucs (~80MB) được demucs tải về cache lần chạy đầu — nếu muốn offline
hoàn toàn, copy sẵn `~/.cache/torch/hub/checkpoints/` vào cạnh binary và trỏ
`TORCH_HOME`. Model basic-pitch (onnx) đã nằm trong package.

## Bảo mật

- Engine là binary PyInstaller — đủ chống đọc lướt; logic nhạy cảm (license,
  entitlement) KHÔNG đặt ở engine, theo đúng mô hình các app G-Labs (server
  quyết định, client chỉ hiển thị).
- Backend Node obfuscate như Video Downloader (`scripts/obfuscate-backend.js`,
  backend/ → server/), frontend obfuscate qua vite plugin + terser.
