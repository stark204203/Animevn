# ANIMEVERSE

**ENTER THE WORLD OF ANIME** — Khám phá thế giới anime, xây dựng thư viện riêng và tiếp tục hành trình của bạn.

AnimeVerse là website React + Vite, thiết kế Mobile First cho điện thoại Android/iPhone. Thư viện ban đầu để trống đúng theo yêu cầu: bạn tự tìm và thêm anime. Metadata được lấy từ AniList GraphQL; AniList không cung cấp tập phim để xem.

## Chức năng trong bản hiện tại

- Trang chủ, thư viện riêng, thể loại, bảng xếp hạng, lịch chiếu và danh sách cá nhân.
- Tìm kiếm / lọc anime bằng AniList: tên, thể loại, năm, mùa, trạng thái, định dạng và cách sắp xếp.
- Nhập thông tin anime từ AniList vào thư viện hoặc tạo mục anime riêng.
- Trang chi tiết anime, poster, ảnh bìa, thể loại, studio, điểm đánh giá, mô tả và trailer nếu AniList có dữ liệu.
- Trang quản lý tập phim: thêm / xóa tập, đặt lịch chiếu, đánh dấu anime nổi bật.
- Trình phát HTML5 cho URL video HTTPS (ví dụ MP4/WebM) và YouTube Embed hợp lệ. Tập chưa có nguồn sẽ hiện thông báo, không phát video giả.
- Tiến độ xem HTML5, tập gần nhất, yêu thích, muốn xem, hồ sơ cục bộ, điểm đánh giá và bình luận được lưu bằng LocalStorage.
- Giao diện responsive, skeleton loading, trạng thái rỗng và thông báo lỗi API.
- Workflow GitHub Actions để build và triển khai GitHub Pages.

## Chạy website

Yêu cầu Node.js 20 trở lên và npm.

```bash
npm install
npm run dev
```

Mở địa chỉ được Vite hiển thị trong terminal (thường là `http://localhost:5173`). Để kiểm tra bản build:

```bash
npm run build
npm run preview
```

## Thêm anime và tập phim

1. Mở **Khám phá** hoặc **Quản lý AnimeVerse**.
2. Nhập tên anime vào ô tìm kiếm AniList.
3. Chọn biểu tượng `+` để đưa anime vào thư viện trên thiết bị.
4. Trong Quản lý AnimeVerse, chọn anime vừa thêm.
5. Nhập số tập, tên tập, loại nguồn và URL video HTTPS hoặc URL YouTube được chủ sở hữu cho phép nhúng.
6. Đánh dấu ô xác nhận bạn có quyền sử dụng nguồn video, sau đó thêm tập.
7. Mở trang chi tiết anime và chọn tập để xem.

Không dùng URL stream lấy từ website không được cấp phép. Với YouTube, ứng dụng chỉ tạo iframe embed từ video ID hợp lệ; quyền nhúng và quyền phân phối vẫn phải do chủ sở hữu nội dung quyết định.

## Dữ liệu và giới hạn bảo mật

Bản này là **frontend tĩnh**. Danh sách anime, tập đã cấu hình, lịch sử, yêu thích, hồ sơ, đánh giá và bình luận đang lưu trong LocalStorage của trình duyệt hiện tại. Dữ liệu không tự đồng bộ sang điện thoại hoặc trình duyệt khác; xóa dữ liệu website có thể làm mất bộ sưu tập.

Hồ sơ hiện tại chỉ là hồ sơ cục bộ, không phải đăng nhập thật. Trang quản lý cũng chưa được bảo vệ bằng xác thực phía máy chủ. Vì vậy:

- Không nhập mật khẩu thật hoặc dữ liệu nhạy cảm vào bản demo.
- Không xem nút quản lý cục bộ là cơ chế phân quyền admin an toàn.
- Trước khi mở cho nhiều người dùng, cần tích hợp Supabase/Firebase hoặc backend riêng cho đăng nhập, database, phân quyền admin, kiểm duyệt bình luận và lưu tiến độ.
- Không lưu khóa bí mật / service-role key trong mã frontend công khai.

## AniList API

Dữ liệu anime được truy vấn qua `https://graphql.anilist.co` bằng GraphQL POST. Nếu AniList giới hạn tốc độ, mất kết nối hoặc thay đổi API, tìm kiếm có thể tạm thời không tải được; hãy đợi rồi thử lại. Anime đã nhập vào thư viện vẫn có thể mở từ dữ liệu đã lưu.

Tài liệu: https://docs.anilist.co/guide/graphql/

## Triển khai lên GitHub Pages bằng điện thoại

1. Tải file ZIP dự án AnimeVerse, giải nén trên điện thoại bằng ứng dụng quản lý tệp.
2. Mở Chrome và truy cập https://github.com/new để tạo repository mới, ví dụ `animeverse`. Chọn Public hoặc Private theo nhu cầu rồi nhấn **Create repository**.
3. Mở repository vừa tạo. Trong giao diện GitHub, chọn **Add file → Upload files**. Tải nội dung bên trong thư mục `animeverse` đã giải nén lên repository (không chỉ tải file ZIP). Giữ nguyên cấu trúc, đặc biệt là thư mục `src`, `public` và `.github/workflows`.
4. Commit các file vào nhánh `main`.
5. Mở **Settings → Pages**. Ở mục **Build and deployment → Source**, chọn **GitHub Actions**.
6. Mở tab **Actions** và chờ workflow **Deploy AnimeVerse to GitHub Pages** chạy thành công. Đường dẫn website sẽ xuất hiện trong mục Pages / phần deployment của workflow.

Mỗi lần bạn commit thay đổi vào `main`, workflow sẽ tự build và cập nhật website. Dự án dùng HashRouter và đường dẫn tài nguyên tương đối để phù hợp với URL dạng `https://TEN-TAI-KHOAN.github.io/animeverse/`.

Nếu giao diện GitHub trên điện thoại không hiển thị chức năng tải cả thư mục, hãy bật **Trang web cho máy tính** trong menu Chrome. Khi tải lên, bắt buộc giữ nguyên thư mục `.github/workflows`; nếu thiếu file `deploy.yml`, GitHub Pages sẽ không tự chạy workflow.

## Cấu trúc chính

```text
animeverse/
├── .github/workflows/deploy.yml
├── public/favicon.svg
├── src/
│   ├── api/anilist.js
│   ├── lib/storage.js
│   ├── App.jsx
│   ├── main.jsx
│   └── styles.css
├── index.html
├── package.json
├── vite.config.js
└── README.md
```

## Các bước để tiến tới bản production

- Kết nối Supabase/Firebase Auth và database có chính sách bảo mật (RLS / security rules).
- Chuyển catalog, episodes, ratings, comments, watch progress sang database; tạo vai trò admin phía server.
- Lưu video trên CDN / nhà cung cấp được cấp phép; kiểm tra quyền truy cập URL ở backend.
- Thêm kiểm duyệt, báo cáo bình luận, giới hạn tốc độ và nhật ký quản trị.
- Bổ sung bộ lọc, trang studio / nhân vật / tin tức khi có nguồn dữ liệu đáng tin cậy.
