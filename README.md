# Nguyễn Thái Bình · Media Link Tree

Trang tổng hợp **189 liên kết** báo chí, video, podcast và bài viết liên quan
Nguyễn Thái Bình (Steven) / Học viện Concepts (VCS).

- **Bài viết:** 151 · **Video:** 31 · **Podcast:** 4 · **Hồ sơ & tổng hợp:** 3
- **Theo năm:** 2026 (86) · 2025 (73) · 2024 (23) · 2023 (4) · Khác (3)
- **Nguồn nhiều nhất:** VietnamBiz, CafeBiz, Znews, Người Lao Động, Mekong ASEAN, Nhịp Cầu Đầu Tư, The Saigon Times

Trang tĩnh 1 file, không backend, không database. Mở bằng trình duyệt là chạy.

---

## 1. Cấu trúc thư mục

```
nguyen-thai-binh-media/
├─ index.html     ← toàn bộ trang (HTML + CSS + JS + dữ liệu link nằm trong 1 file)
├─ README.md      ← file này
└─ .gitignore     ← chặn file rác OneDrive/Windows/macOS lọt vào repo
```

> `index.html` là tên bắt buộc để Cloudflare Pages nhận làm trang gốc.
> File gốc `VCS_Nguyen_Thai_Binh_Media_LinkTree_AutoImport_Clean.html` đã được đổi tên sang đây.

---

## 2. Deploy lên Cloudflare Pages qua GitHub (không cần cài git)

Toàn bộ làm trên web, kéo-thả file. Khoảng 10 phút.

### Bước 1 — Tạo repo trên GitHub

1. Vào **github.com** → nút **+** góc phải trên → **New repository**
2. Điền:
   - **Repository name:** `nguyen-thai-binh-media`
   - **Visibility:** `Public` (Cloudflare Pages bản free đọc được repo private, nhưng Public đơn giản hơn)
   - **KHÔNG** tick "Add a README file" (đã có sẵn trong thư mục này rồi)
3. **Create repository**

### Bước 2 — Upload 3 file

1. Ở màn hình repo vừa tạo, bấm link **uploading an existing file**
   (hoặc **Add file** → **Upload files**)
2. Mở thư mục `nguyen-thai-binh-media` trên máy, **chọn cả 3 file** (`index.html`, `README.md`, `.gitignore`) rồi kéo thả vào ô upload

   > `.gitignore` bắt đầu bằng dấu chấm nên Windows Explorer có thể ẩn đi.
   > Nếu không thấy: tab **View** → tick **Hidden items**.

3. Ô **Commit changes** ghi: `Initial commit - VCS Media Link Tree`
4. Bấm **Commit changes**

### Bước 3 — Nối Cloudflare Pages với GitHub

1. Vào **dash.cloudflare.com** → menu trái: **Workers & Pages**
2. **Create** → tab **Pages** → **Connect to Git**
3. **Connect GitHub** → đăng nhập → chọn **Only select repositories** → chọn `nguyen-thai-binh-media` → **Install & Authorize**
4. Chọn repo `nguyen-thai-binh-media` → **Begin setup**

### Bước 4 — Cấu hình build (quan trọng: để TRỐNG)

Đây là trang HTML tĩnh, không cần build gì cả:

| Trường | Điền |
|---|---|
| Project name | `nguyen-thai-binh-media` |
| Production branch | `main` |
| Framework preset | **None** |
| Build command | **để trống** |
| Build output directory | `/` (hoặc để trống) |

Bấm **Save and Deploy**. Chờ ~1 phút.

### Bước 5 — Nhận link

Xong, trang sẽ live tại:

```
https://nguyen-thai-binh-media.pages.dev
```

> Nếu tên project đã có người dùng, Cloudflare tự thêm hậu tố.
> Kiểm tra link thật ở tab **Deployments** trong project.

---

## 3. Gắn tên miền riêng (tuỳ chọn)

Ví dụ muốn dùng `media.vcs.edu.vn`:

1. Trong project Pages → tab **Custom domains** → **Set up a custom domain**
2. Nhập `media.vcs.edu.vn` → **Continue**
3. **Nếu vcs.edu.vn đã nằm trong Cloudflare:** bấm **Activate domain**, xong.
4. **Nếu chưa:** Cloudflare sẽ hiện 1 bản ghi `CNAME` → vào nhà cung cấp tên miền, thêm:

   | Type | Name | Value |
   |---|---|---|
   | CNAME | `media` | `nguyen-thai-binh-media.pages.dev` |

5. Chờ DNS lan truyền (5 phút – 24 giờ). SSL Cloudflare cấp tự động.

**Sau khi đổi sang tên miền riêng**, sửa 3 dòng trong `index.html` cho khớp URL mới
(ảnh hưởng SEO và preview khi share link):

```html
<link rel="canonical" href="https://media.vcs.edu.vn/">
<meta property="og:url" content="https://media.vcs.edu.vn/">
...trong khối <script type="application/ld+json"> : "url":"https://media.vcs.edu.vn/"
```

---

## 4. Cập nhật danh sách link sau này

Trang có sẵn 2 nút quản trị, chạy **hoàn toàn trong trình duyệt** — không gửi dữ liệu đi đâu:

1. Mở trang (bản live hoặc file trên máy)
2. **Nhập từ file Word (.docx)** → chọn file Word chứa danh sách link mới
   → trang tự bóc hyperlink, nhận diện nguồn, phân nhóm và phân năm
3. Kiểm tra bằng mắt xem số link và phân nhóm đã đúng
4. **Xuất HTML mới** → tải về `VCS_Nguyen_Thai_Binh_Media_LinkTree_Updated.html`
5. Đổi tên file vừa tải thành **`index.html`**
6. Lên GitHub → mở `index.html` → biểu tượng **bút chì** → xoá hết nội dung cũ, dán nội dung mới
   → **Commit changes**

   > Cách nhanh hơn: **Add file** → **Upload files** → kéo `index.html` mới vào,
   > GitHub tự ghi đè file trùng tên.

7. Cloudflare Pages tự deploy lại trong ~1 phút. Không cần làm gì thêm.

> **Lưu ý khi export:** file tải về mang tên `..._Updated.html`.
> Bắt buộc đổi thành `index.html` trước khi đẩy lên, nếu không Cloudflare
> sẽ không nhận làm trang chủ và link sẽ báo 404.

---

## 5. Ghi chú kỹ thuật

- **Phụ thuộc ngoài duy nhất:** `jszip@3.10.1` từ cdn.jsdelivr.net — chỉ dùng cho
  chức năng đọc file `.docx`. Nếu CDN chết, phần hiển thị link vẫn chạy bình thường.
- **Dữ liệu link** nằm trong biến `DATA` (mảng JSON) ngay trong `index.html`.
  Có thể sửa tay nếu cần đổi 1–2 link lẻ.
- Đã bổ sung so với file gốc: thẻ `canonical`, `robots`, Open Graph, Twitter Card,
  favicon và `schema.org/ProfilePage` — để khi share link lên Facebook/Zalo có
  tiêu đề + mô tả tử tế, và Google hiểu đây là trang hồ sơ cá nhân.
- Mọi link ra ngoài đều có `target="_blank"` + `rel="noopener"`.

---

*Học viện Concepts (VCS) — vcs.edu.vn*
