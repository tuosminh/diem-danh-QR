# Điểm danh nhân viên bằng QR

Website tĩnh để hiển thị mã QR cá nhân và quét mã điểm danh. Giao diện được lưu trữ bằng GitHub Pages; việc xác thực và lưu dữ liệu vẫn do Google Apps Script xử lý.

## Triển khai lên GitHub Pages

Repo này có GitHub Actions workflow triển khai tự động nội dung `index.html` lên GitHub Pages mỗi khi có thay đổi trên nhánh `main`.

1. Mở repo **Settings → Pages**.
2. Ở mục **Build and deployment**, chọn **Source: GitHub Actions**.
3. Đẩy thay đổi lên nhánh `main` hoặc chạy workflow **Deploy to GitHub Pages** trong tab **Actions**.
4. Chờ workflow hoàn tất, sau đó mở địa chỉ dạng `https://tuosminh.github.io/diem-danh-QR/` (có thể xem URL chính xác trong **Settings → Pages**).

## Google Apps Script

GitHub Pages chỉ lưu trữ HTML, CSS và JavaScript tĩnh; nó không chạy máy chủ và không thay thế backend. Trang này cần một Google Apps Script đã triển khai dưới dạng web app để kiểm tra PIN, xác thực mã QR và ghi điểm danh vào Google Sheets.

- Kiểm tra `SCRIPT_URL` trong `index.html` là URL triển khai Apps Script kết thúc bằng `/exec`.
- Đảm bảo Apps Script và bảng tính đã được cấu hình, và quyền truy cập của web app phù hợp với quy trình nội bộ.
- Không đưa PIN kiểm soát hoặc thông tin bí mật vào mã nguồn. PIN được nhập tại trang quét.
- Camera chỉ hoạt động trên HTTPS (GitHub Pages hỗ trợ HTTPS) hoặc `localhost`. Cần cấp quyền camera và kết nối Internet để tải thư viện QR.
- Để thử điểm danh, dùng mã QR hợp lệ của một nhân viên kiểm thử và PIN đúng. Lượt quét sẽ được ghi vào Google Sheets; sau khi xác nhận, có thể xóa riêng dòng kiểm thử trên sheet. Không xóa dòng của lượt điểm danh thật. Nếu Apps Script có lưu trạng thái chống trùng riêng ngoài sheet, cần xóa trạng thái đó theo cách cấu hình của Apps Script trước khi quét lại mã kiểm thử.

Thay đổi `index.html` rồi đẩy lên `main` để website được triển khai lại tự động.
