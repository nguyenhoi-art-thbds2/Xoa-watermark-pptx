# Xóa watermark Gemini Notebook trong file PowerPoint

Công cụ chạy **hoàn toàn trên trình duyệt** để xóa logo và chữ "Gemini Notebook" nằm trong ảnh của các slide (file `.pptx`). File không bị tải lên máy chủ nào, file gốc luôn được giữ nguyên.

Phát triển bởi thầy Hợi · Trường Tiểu học Bảo Đài 2 - TP Bắc Ninh · [0967 834 824](tel:0967834824)

## Tính năng

- Chọn **cả thư mục** chứa file `.pptx` (Chrome/Edge) hoặc chọn từng file. Kết quả lưu vào thư mục con `da_xoa_watermark`.
- **Cường độ xóa** từ 0 đến 100%. Mức 100% xóa sạch toàn bộ vùng đã chọn.
- **Cửa sổ xem trước**: kéo chuột để vẽ hoặc di chuyển vùng xóa, xem ảnh Trước/Sau, chuyển qua lại giữa các slide.
- Có nút **Bắt đầu**, thanh tiến độ và nút **Xóa file khác** để làm đợt mới.
- Tự xử lý ảnh nền tối (viền thiết bị màu đen) và xóa cả phần watermark nằm trong kênh trong suốt (alpha) của ảnh PNG.

## Cách dùng

1. Mở trang web của công cụ bằng **Chrome hoặc Edge**.
2. Bấm **Chọn thư mục chứa file .pptx** (hoặc **Hoặc chọn từng file**).
3. (Tùy chọn) Bấm **Xem trước và chọn vùng xóa** để chỉnh vùng, chỉnh cường độ.
4. Bấm **Xóa watermark** và chờ thanh tiến độ chạy xong.
5. Bấm **Xóa file khác** nếu muốn làm đợt file mới.

## Triển khai lên GitHub Pages

**Cách 1: tải lên bằng giao diện web (không cần dùng lệnh)**

1. Đăng nhập GitHub, bấm **New repository**, đặt tên (ví dụ `xoa-watermark-pptx`), chọn **Public**, bấm **Create repository**.
2. Bấm **uploading an existing file**, kéo thả **toàn bộ nội dung** của thư mục này (gồm `index.html`, `css`, `js`, `assets`, `.nojekyll`, `README.md`) vào, rồi bấm **Commit changes**.
   Lưu ý: `index.html` phải nằm ở thư mục gốc của repo, không nằm trong thư mục con.
3. Vào **Settings → Pages**. Ở mục **Build and deployment**, chọn **Source: Deploy from a branch**, **Branch: main**, thư mục **/(root)**, bấm **Save**.
4. Chờ 1 đến 2 phút. Địa chỉ trang sẽ là `https://<tên-tài-khoản>.github.io/<tên-repo>/`.

**Cách 2: dùng Git**

```bash
git init
git add .
git commit -m "Công cụ xóa watermark pptx"
git branch -M main
git remote add origin https://github.com/<tên-tài-khoản>/<tên-repo>.git
git push -u origin main
```

Sau đó làm bước 3 và 4 ở Cách 1.

**Chạy thử trên máy:** mở trực tiếp file `index.html` bằng Chrome/Edge, hoặc chạy `python -m http.server` trong thư mục này rồi mở `http://localhost:8000`.

## Cấu trúc thư mục

```
index.html          Giao diện
css/style.css       Kiểu dáng
js/app.js           Xử lý chính (xóa watermark, xem trước, tiến độ)
js/jszip.min.js     Thư viện JSZip để đọc/ghi file .pptx (đã kèm sẵn, không cần mạng)
assets/             Logo và biểu tượng của trang
.nojekyll           Báo GitHub Pages phục vụ file nguyên trạng
```

## Tùy chỉnh

- **Vùng xóa mặc định** nằm ở bốn ô `bx1`, `by1`, `bx2`, `by2` trong `index.html` (tọa độ pixel trên ảnh 1376×768), và ở nút "Đặt lại mặc định" trong `js/app.js`.
- Công cụ chỉ xử lý ảnh PNG kích thước **1376×768**. Ảnh khác kích thước được bỏ qua.
- Muốn đổi logo: thay các file trong thư mục `assets/` (giữ nguyên tên file).

## Ghi chú

- Cần trình duyệt có hỗ trợ chọn thư mục (Chrome, Edge). Trình duyệt khác vẫn dùng được bằng "Chọn từng file", kết quả sẽ được tải xuống với tiền tố `sach_`.
- Thư viện [JSZip](https://stuk.github.io/jszip/) (MIT/GPLv3) được dùng để đọc và ghi file `.pptx`.
