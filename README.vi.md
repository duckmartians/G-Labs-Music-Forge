<h1 align="center">G-Labs Music Forge</h1>

<p align="center"><b>Ứng dụng desktop miễn phí biến một bài hát thành nhạc không lời, stems, MIDI giai điệu, hợp âm/tông/tempo và sheet nhạc phát được - xử lý offline hoàn toàn trên máy của bạn.</b></p>

<p align="center">
  <a href="README.md">English</a> ·
  <b>Tiếng Việt</b>
</p>

<p align="center">
  <a href="https://github.com/duckmartians/G-Labs-Music-Forge/releases/latest"><img alt="Tải về cho Windows" src="https://img.shields.io/badge/T%E1%BA%A3i%20v%E1%BB%81-Windows-0078D6?style=for-the-badge&logo=windows&logoColor=white"></a>&nbsp;
  <a href="https://github.com/duckmartians/G-Labs-Music-Forge/releases/latest"><img alt="Tải về cho macOS (Apple Silicon)" src="https://img.shields.io/badge/T%E1%BA%A3i%20v%E1%BB%81-macOS%20Apple%20Silicon-000000?style=for-the-badge&logo=apple&logoColor=white"></a>
</p>

---

## Cài đặt

### Bước 1 - Chọn đúng bản cho máy của bạn

Tải bản mới nhất từ **[Releases](https://github.com/duckmartians/G-Labs-Music-Forge/releases/latest)**, rồi chọn tệp theo đúng máy:

| Máy của bạn | Tải tệp | Ghi chú |
|---|---|---|
| 🪟 **Windows 10/11 (64-bit)** | [`GLabsMusicForge-<phiên bản>-setup.exe`](https://github.com/duckmartians/G-Labs-Music-Forge/releases/latest) | Bộ cài. Engine chạy bằng CPU, không cần card đồ hoạ |
| 🍎 **Mac chip Apple (M1/M2/M3/M4)** | [`GLabsMusicForge-<phiên bản>-arm64.dmg`](https://github.com/duckmartians/G-Labs-Music-Forge/releases/latest) | Tách stem được tăng tốc GPU |

> **Chưa có bản cho Mac chip Intel.** Bản arm64 sẽ không mở được trên máy Intel.

### Bước 2 - Cài đặt

<details open>
<summary><b>🪟 Trên Windows</b></summary>

1. Mở tệp **`GLabsMusicForge-<phiên bản>-setup.exe`** vừa tải.
2. Nếu hiện bảng **"Windows protected your PC"** (SmartScreen): bấm **More info** → **Run anyway**. *(App chưa mua chứng chỉ ký của Microsoft nên bị cảnh báo - không phải virus.)*
3. Làm theo trình cài đặt. Bạn có thể đổi thư mục cài nếu muốn.
4. Mở app từ **Start Menu** hoặc lối tắt trên **Desktop**.

</details>

<details open>
<summary><b>🍎 Trên macOS</b></summary>

1. Mở tệp **`.dmg`** vừa tải, rồi **kéo biểu tượng G-Labs Music Forge thả vào thư mục Applications**.
2. Vào **Applications**, **bấm chuột phải** (hoặc giữ Control rồi bấm) lên **G-Labs Music Forge** → chọn **Open** → bấm **Open** lần nữa ở hộp xác nhận. *(App chưa được Apple ký nên phải mở kiểu này ở **lần đầu**; những lần sau mở bình thường như mọi app.)*
3. Nếu macOS báo **"bị hỏng / không thể mở"** hoặc không thấy nút Open, mở **Terminal** và dán lệnh sau rồi Enter:
   ```bash
   xattr -dr com.apple.quarantine "/Applications/G-Labs Music Forge.app"
   ```
   Sau đó mở lại app.

</details>

### Bước 3 - Không cần tài khoản

Music Forge **miễn phí**: không có gói trả phí, không mã bản quyền, không cần đăng nhập. Mô hình AI (Demucs, basic-pitch) và FFmpeg đã nằm sẵn trong bộ cài, nên không phải cài Python hay FFmpeg, và việc phân tích chạy được cả khi không có Internet.

Ứng dụng **tự cập nhật**: khi khởi động nó kiểm tra GitHub Releases, và huy hiệu phiên bản cho phép tải bản mới ngay trong app. Trên Windows trình cài đặt sẽ chạy rồi mở lại app; trên macOS app đóng lại và mở tệp `.dmg` mới - kéo app vào Applications để thay bản cũ, rồi mở lại.

---

## Lần chạy đầu tiên

1. **Mở ứng dụng.** Chấm engine trên thanh tiêu đề chuyển xanh khi engine phân tích đã sẵn sàng.
2. **Thêm bản nhạc** - kéo thả hoặc bấm **Chọn file**: file nhạc (MP3, WAV, M4A, AAC, FLAC, OGG, OPUS, WEBM, AIFF, WMA) hoặc MIDI (`.mid`, `.midi`). Thêm được nhiều file cùng lúc.
3. **Chọn trích xuất gì** - Nhạc không lời & vocal, Giai điệu → MIDI, Hợp âm, tông & tempo, Sheet nhạc; chọn nguồn chép sheet và độ chi tiết nốt.
4. Bấm **Bắt đầu xử lý** và theo dõi tiến độ từng bài ở **Các bản phân tích**.
5. Khi bài báo **Xong**, bấm **Xem kết quả** để nghe thử, nghe theo hợp âm, phát sheet, hoặc mở thư mục rồi kéo tệp thẳng vào DAW.

---

## Tính năng

![G-Labs Music Forge](docs/screenshots/01-main.png)

- **Tách stem & nhạc không lời** - Demucs tách vocal / trống / bass / nhạc cụ khác. Bản nhạc không lời tạo bằng cách trừ vocal khỏi bản gốc, nên phần nhạc giữ nguyên chất lượng. Bật **Giữ đủ các stem** để lấy thêm trống, bass và nhạc cụ khác.
- **Giai điệu → MIDI** - basic-pitch chép giai điệu hát thành một dòng lead một bè (`melody.mid`). Cổng năng lượng vocal chặn tiếng sót sau tách sinh nốt "ma" ở những đoạn không ai hát.
- **Nguồn chép sheet & độ chi tiết nốt** - chép sheet từ **Tự động · Vocal · Nhạc · Cả bài**, kèm độ chi tiết **Gọn / Chuẩn / Chi tiết** đánh đổi luyến láy lấy độ dễ đọc.
- **Hợp âm, tông & tempo** - vòng hợp âm theo nhịp với chế độ nghe kèm: nhạc không lời chạy bên dưới, hợp âm đang phát sáng lên, bấm hợp âm bất kỳ để nhảy đến đúng đoạn.
- **Sheet nhạc biết tự chơi** - MusicXML khắc ngay trong app; piano chơi đúng từng nốt trên sheet, nốt đang phát sáng lên và trang tự cuộn theo. Tốc độ phát 0.5-1.5× (giữ nguyên cao độ) và zoom.
- **Hàng chờ nhiều bài** - thêm nhiều file, rồi **Bắt đầu xử lý / Tạm dừng** (bài đang chạy hoàn tất nốt) **/ Dừng hẳn** (huỷ luôn bài đang chạy).
- **Tạo lại theo tuỳ chọn hiện tại** - tick thêm mục trích xuất rồi bấm ↻ ở bài đã xong, hoặc kéo khung chọn nhiều hàng (Shift cộng, Alt trừ) rồi **Chạy mục đã chọn**.
- **Dùng MIDI có sẵn** - thả tệp `.mid` vào là app dựng sheet và bản piano nghe thử thẳng từ đó, không cần tách stem.
- **Kết quả sẵn cho DAW** - mỗi bài một thư mục gồm MP3 nhạc không lời/stems, `melody.mid`, `sheet.mid` đã quantize, `sheet.musicxml`, `chords.json` và bản piano nghe thử MP3.
- **Cục bộ & riêng tư** - mọi thứ chạy trên máy bạn, không tải gì lên. Mạng chỉ dùng để kiểm tra bản cập nhật.
- **6 ngôn ngữ** - English, Tiếng Việt, 简体中文, Español, العربية (phải sang trái), Русский.

---

## Các trang

### 🎛 Cửa sổ chính - thêm bài &amp; hàng chờ

![Hàng chờ đang chạy](docs/screenshots/05-queue-running.png)

Thêm bài ở bên trái, chọn **Trích xuất gì**, các bài sẽ vào **Các bản phân tích**. Mỗi hàng hiện bước đang chạy (giải mã, tách stem, chép giai điệu, khắc sheet…) và tiến độ. Từ mỗi hàng bạn có thể xem kết quả, mở thư mục, tạo lại theo tuỳ chọn hiện tại, huỷ hoặc xoá khỏi danh sách. **Nhật ký hoạt động** sao chép hoặc xuất ra được, còn **Cài đặt** chứa thư mục kết quả.

### 🎧 Nghe thử

![Nghe thử](docs/screenshots/02-listen.png)

Nghe nhạc không lời, vocal và (nếu giữ) trống, bass, nhạc cụ khác, kèm nút tải từng tệp và bản piano nghe thử giai điệu.

### 🎸 Hợp âm

![Hợp âm](docs/screenshots/03-chords.png)

Tông, tempo và vòng hợp âm theo nhịp. Bấm **Nghe theo hợp âm**: nhạc không lời phát, hợp âm đang chơi sáng lên, bấm hợp âm bất kỳ để nhảy đến đoạn đó.

### 🎼 Sheet nhạc

![Sheet nhạc](docs/screenshots/04-sheet.png)

Bản MusicXML đã khắc. **Nghe thử sheet này** cho piano chơi đúng những gì được viết, có chỉnh tốc độ (0.5×-1.5×) và zoom. Bản chép là bản phác thảo có chủ đích - hãy xem như nháp để chỉnh tiếp, chưa phải sheet hoàn chỉnh.

### 📁 Tệp

Mọi tệp đầu ra của bài (MP3, `melody.mid`, `sheet.mid`, `sheet.musicxml`, `chords.json`) kèm nút **Tải về** và **Hiện trong thư mục**.

### 🌐 Ngôn ngữ

![Tiếng Ả Rập (RTL)](docs/screenshots/06-rtl-arabic.png)

Đổi ngôn ngữ giao diện bất kỳ lúc nào; tiếng Ả Rập dùng bố cục phải sang trái đầy đủ.

---

## Cách hoạt động

```
bài hát.mp3 ──► giải mã ──► hợp âm/tông/tempo (chroma + Viterbi)
                    │
                    ├──► Demucs tách stem ──► nhạc không lời = bản gốc − vocal
                    │
                    └──► basic-pitch (ONNX) ──► melody.mid ──► quantize ──► sheet.musicxml
                                                        └──► piano nghe thử (render từ bản ĐÃ
                                                             quantize - nghe gì thấy nấy trên sheet)
```

Đoạn rap vốn dĩ chép ra dày nốt; độ chi tiết **Gọn** hợp nhất ở đó.

---

## Nơi lưu dữ liệu

| Gì | macOS | Windows |
|---|---|---|
| Kết quả (mỗi bài một thư mục `<tên bài>_<thời điểm>`) | `~/Documents/G-Labs Music Forge` | `%USERPROFILE%\Documents\G-Labs Music Forge` |
| Cài đặt (`settings.json`) | `~/Library/Application Support/G-Labs Music Forge` | `%APPDATA%\G-Labs Music Forge` |

Đổi thư mục kết quả ở **Cài đặt → Thư mục kết quả**.

---

## Khắc phục sự cố

**"Không tìm thấy engine phân tích - hãy cài lại ứng dụng"** - engine đi kèm bị thiếu hoặc hỏng. Tải bản mới nhất từ [Releases](https://github.com/duckmartians/G-Labs-Music-Forge/releases/latest) và cài lại.

**Sheet quá nhiều nốt / rối** - chọn độ chi tiết **Gọn**, hoặc thử nguồn chép khác (ví dụ **Vocal**), rồi bấm ↻ để chạy lại bài.

**Tách stem chậm trên Windows** - trên Windows engine chạy bằng CPU; chỉ Mac Apple Silicon được tăng tốc GPU.

**Windows chặn ở "Windows protected your PC"** - bấm **More info → Run anyway**. App chưa mua chứng chỉ ký nên bị cảnh báo, không phải virus.

**macOS báo ứng dụng bị hỏng / không mở được** - app chưa được Apple ký. Chuột phải → **Open** ở lần đầu, hoặc chạy `xattr -dr com.apple.quarantine "/Applications/G-Labs Music Forge.app"`.

**Bản cập nhật không cài được** - tải bản mới nhất thủ công từ [Releases](https://github.com/duckmartians/G-Labs-Music-Forge/releases/latest).

> Bạn chịu trách nhiệm về quyền sử dụng bài hát mình xử lý và cách dùng kết quả.
