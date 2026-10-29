# Thượng Hải 23–28/12/2026 🏮

Trang xem nhanh kế hoạch chuyến đi của nhóm. Mọi dữ liệu được lấy trực tiếp từ Google Sheet mỗi lần mở trang, nên chỉ cần sửa sheet là web tự cập nhật.

- Web: https://vmttri-glitch.github.io/shanghai-trip/
- Sửa dữ liệu: Google Sheet "Kế hoạch du lịch Thượng Hải 23–28/12/2026" (nút ✏️ trên trang)

Lưu ý: sheet cần để chế độ "Bất kỳ ai có đường liên kết → Người xem". Không đưa số hộ chiếu, CCCD vào sheet này vì web là công khai.

## Ô "Hỏi & ghi nhanh" (AI)

Mọi người gõ tự nhiên trên web, ví dụ "Ly đã trả ks 100000" (AI ghi vào tab **Sổ thu chi**) hoặc "Mấy giờ bay về?" (AI trả lời từ dữ liệu sheet). AI chạy bằng GitHub Models qua một Apps Script gắn trong sheet; không có khóa nào nằm trên web.

Cài một lần (người giữ sheet làm):

1. **Tạo token GitHub**: https://github.com/settings/personal-access-tokens/new → đặt tên, hạn 90 ngày → *Permissions → Account permissions → Models: Read-only* → Generate → chép token.
2. **Dán script**: mở Google Sheet → *Tiện ích mở rộng → Apps Script* → xóa nội dung có sẵn → dán toàn bộ `apps-script/ghi-nhanh.gs` → Lưu.
3. **Thêm 2 thuộc tính**: *Cài đặt dự án (⚙️) → Thuộc tính tập lệnh*:
   - `GITHUB_TOKEN` = token ở bước 1
   - `PASSCODE` = một mã nhóm tự đặt (gửi mã này cho cả nhóm)
4. **Thử**: chọn hàm `thu` → ▶ Chạy → cấp quyền khi được hỏi → xem kết quả ở Nhật ký thực thi.
5. **Triển khai**: *Triển khai → Tùy chọn triển khai mới → Ứng dụng web*; Thực thi với tư cách: **Tôi**; Ai có quyền truy cập: **Bất kỳ ai** → Triển khai → chép **URL ứng dụng web** (kết thúc bằng `/exec`).
6. Dán URL đó vào `APPS_SCRIPT_URL` trong `index.html`.

An toàn: chỉ ai biết `PASSCODE` mới gửi được; tối đa 40 lượt/10 phút; AI chỉ *thêm dòng* vào Sổ thu chi, không sửa tab khác, và không đọc sheet hộ chiếu. Ai có quyền **sửa** sheet thì xem được script và token, nên chỉ cấp quyền sửa cho người trong nhóm (token chỉ có quyền gọi AI).
