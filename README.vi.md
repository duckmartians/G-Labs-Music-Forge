# G-Labs Music Forge

[English](README.md) | **Tiếng Việt**

Ứng dụng desktop "rèn" một bản nhạc (MP3, WAV, M4A, FLAC… hoặc MIDI) thành nguyên liệu sáng tác — **nhạc không lời & stems, MIDI giai điệu, hợp âm/tông/tempo, và sheet nhạc phát được** — xử lý hoàn toàn trên máy của bạn. Sinh ra cho quy trình nhạc AI: giữ phần nhạc bạn ưng, bỏ phần lời chưa ưng, lấy "ADN âm nhạc" để viết tiếp.

![Màn hình chính](docs/screenshots/01-main.png)

## Tính năng

- **Tách stem (Demucs)**: vocal / trống / bass / nhạc cụ khác — và bản **nhạc không lời** thật sự tạo bằng cách trừ vocal khỏi bản gốc, nên phần nhạc giữ nguyên chất lượng
- **Giai điệu → MIDI** (basic-pitch): chép giai điệu hát thành dòng lead một bè; **cổng năng lượng vocal** chặn tiếng nhạc sót sau tách (bleed) sinh nốt "ma" ở những đoạn không ai hát
- **Chọn nguồn chép sheet**: Tự động · Vocal · Nhạc · Cả bài — kèm thang **độ chi tiết nốt** (Gọn / Chuẩn / Chi tiết) đánh đổi luyến láy lấy độ dễ đọc
- **Hợp âm, tông & tempo**: vòng hợp âm theo nhịp với chế độ nghe kèm — nhạc không lời chạy bên dưới, **hợp âm đang phát sáng lên**, bấm hợp âm bất kỳ để nhảy đến đúng đoạn
- **Sheet nhạc biết tự chơi**: MusicXML khắc ngay trong app; bấm phát là piano chơi **đúng từng nốt trên sheet**, nốt đang phát sáng lên và trang tự cuộn theo — kèm **tốc độ phát** (0.5–1.5×, giữ nguyên cao độ) và zoom (50–160%)
- **Hàng chờ như trình tải video**: thêm nhiều file một lượt (chọn nhiều, kéo thả), rồi Bắt đầu / Tạm dừng (mềm — bài đang chạy hoàn tất nốt) / Dừng hẳn (huỷ luôn); tiến độ từng bài hiển thị trên chính chiếc slider của icon app
- **Tạo lại theo tuỳ chọn hiện tại**: tick thêm mục trích xuất, bấm ↻ ở bài đã xong — hoặc **quét chọn** nhiều hàng (kéo khung, Shift cộng, Alt trừ) và chạy lại cả loạt
- **Mọi thứ nằm trên đĩa**: mỗi bài một thư mục kết quả gồm MP3 nhạc không lời/stems, `melody.mid`, `sheet.mid` đã quantize, `sheet.musicxml`, `chords.json` và bản piano nghe thử — kéo thẳng vào DAW
- **Cục bộ & riêng tư**: phân tích chạy offline trên máy bạn (tăng tốc GPU Apple Silicon); không tải gì lên đâu cả
- **Tự cập nhật**: kiểm tra GitHub Releases, tải và cài ngay trong app
- **6 ngôn ngữ**: English, Tiếng Việt, 简体中文, Español, العربية (RTL), Русский

## Ảnh màn hình

| Nghe thử — stems kèm nút tải từng file | Hợp âm — nghe kèm, hợp âm đang phát sáng |
|---|---|
| ![Nghe thử](docs/screenshots/02-listen.png) | ![Hợp âm](docs/screenshots/03-chords.png) |

| Sheet nhạc — tự chơi, chỉnh tốc độ & zoom | Hàng chờ đang chạy |
|---|---|
| ![Sheet](docs/screenshots/04-sheet.png) | ![Hàng chờ](docs/screenshots/05-queue-running.png) |

| RTL (العربية) |
|---|
| ![RTL](docs/screenshots/06-rtl-arabic.png) |

## Cách hoạt động

```
bài hát.mp3 ──► giải mã ──► hợp âm/tông/tempo (chroma + Viterbi)
                    │
                    ├──► Demucs tách stem ──► nhạc không lời = bản gốc − vocal
                    │
                    └──► basic-pitch (ONNX) ──► melody.mid ──► quantize ──► sheet.musicxml
                                                        └──► piano nghe thử (render từ bản ĐÃ
                                                             quantize — nghe gì thấy nấy trên sheet)
```

Bản chép là bản phác thảo có chủ đích — hãy xem như nháp để tinh chỉnh tiếp, chưa phải sheet hoàn chỉnh. Đoạn rap vốn dĩ chép ra dày nốt; mức **Gọn** là bạn đồng hành đúng nhất ở đó.

## Cài đặt

Tải bản mới nhất tại [Releases](https://github.com/duckmartians/G-Labs-Music-Forge/releases):

- **Windows**: `GLabsMusicForge-<phiên bản>-setup.exe`
- **macOS (Apple Silicon)**: `GLabsMusicForge-<phiên bản>-arm64.dmg` — chưa ký; lần mở đầu: chuột phải → Open, hoặc `xattr -dr com.apple.quarantine "/Applications/G-Labs Music Forge.app"`

Thiết lập lưu ở thư mục dữ liệu người dùng của hệ điều hành (`%APPDATA%\G-Labs Music Forge` trên Windows, `~/Library/Application Support/G-Labs Music Forge` trên macOS). Kết quả mặc định vào `Documents/G-Labs Music Forge`.

