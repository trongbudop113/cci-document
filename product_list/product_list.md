# Product Listing Generate UI Spec

## Mục Tiêu
- Chuẩn hoá tài liệu để Generate UI/UX, AI tool hiểu và sinh code hiển thị danh sách sản phẩm đúng theo design.
- Định nghĩa rõ loại item, thuật ngữ layout, quy tắc hiển thị ảnh/video, hiệu ứng và cấu trúc dữ liệu để dựng UI/logic nhất quán cho các block danh sách sản phẩm liên quan.

## Phạm Vi Áp Dụng
- Màn hình danh sách sản phẩm dạng lưới 2 cột; có thể xen kẽ banner slider và mục thông tin bổ ích.
- Nền tảng: Web và App.

## Thuật Ngữ Về Khoảng Cách, Kích Thước
- Đơn vị: 
    - `px` làm chuẩn chung để tính khoảng cách
    - `sp` để tính kích thước chữ
- Thuật ngữ dùng chung:
    - `margin` khoảng cách bên ngoài viền của 1 phần tử
    - `padding` khoảng cách bên trong viền
    - `line-height` khoảng cách giữa các dòng chữ
    - `gap` khoảng cách giữa các component
    - `border-radius` bo viền 
    - `font-size` kích thước chữ
    - `font-weight` cỡ chữ
    
## Loại Item hiển thị
- Thông tin bổ ích (xen kẽ)
- Banner quảng cáo dạng slide (xen kẽ)
- Sản phẩm
  - Sản phẩm thường
  - Sản phẩm kèm quà tặng
  - Sản phẩm digital

## Thành Phần Mỗi Product Item
- Banner dạng quảng cáo (//Todo: Trân xem xét nên mô tả mục này ko?)
  - Vị trí hiển thị
  - Xử lý hiển thị hình ảnh (//Todo: Anh Hòa, Thanh iOS), full item, tỉ lệ 177 x 288
  - Dạng slide chuyển từ trái sang phải
- Thông tin bổ ích (//Todo: Trân xem xét nên mô tả mục này ko?)
  - Vị trí hiển thị
  - Dạng slide chuyển từ trái sang phải
- Sản phẩm
  - Khoảnh cách và kích thước:
    - margin: `5px`
    - padding: `6px`
    - font-size: `13sp` cho title, `12sp` cho oldPrice, `16sp` cho currentPrice
    - line-height: `16 / 13`
    - gap từ ảnh sản phẩm tới title: `6px`
    - gap từ title tới cụm đánh giá: `12px`
    - gap từ cụm đánh giá tới cụm price: `12px`
  - Media: ảnh hoặc video khung 1:1
  - Label: “FREESHIP”, “siêu tốc 1h”.
  - Frame: Khung chương trình khuyến mãi
  - Tiêu đề: tối đa 2 dòng, hiển thị ... khi tiêu dề dài vượt quá 
  (ellipsis).
  - Thông tin phụ: brand/cửa hàng/khoảng cách giao, tối đa 1 dòng.
  - Giá:
    - `oldPrice` tùy chọn (strikethrough)
    - `discountPercent`/`discountValue` nếu có
    - `currentPrice` luôn có
  - Đánh giá & đã bán:
    - Đánh giá từ 1 - 5 sao
    - “Đã bán x” rút gọn: `1.2k`, `2.4k+`
  - Badge count hiển thị khi có sản phẩm thêm vào giỏ hàng và nằm góc phải trên cùng nút `Thêm vào giỏ`:
    - font-size: `11sp`
    - background màu `#FF6400`
    - border-radius `10px`
  - Background khuyến mãi đơn hàng
  - Hành động : Thêm vào giỏ, xem chi tiết.

## Xử Lý Ảnh Sản Phẩm
- Khung media: tỉ lệ là 1:1.
    - Case `height = width` hiển thị ảnh nằm trọn trong khung
    - Case `height > width` hiển thị ảnh căn theo max height
    - Case `height < width` hiển thị ảnh căn theo max width
- Placeholder:
  - Khi chưa tải: nền xám nhạt + shimmer
  - Khi lỗi: hiển thị logo ConCung giữa nền trắng
- Tối ưu:
  - Prefetch khi item sắp vào viewport
  - Caching theo `id/url` + kích thước khung

## Xử Lý Video
- Poster: thumbnail tĩnh trong khung 1:1; overlay icon play ở giữa.
- Auto‑play: tắt trong danh sách; chỉ phát khi người dùng nhấn.
- Khi phát inline:
  - Mute mặc định; pause khi item rời viewport hoặc khi cuộn.
- Tài nguyên:
  - Dùng player native, bật hardware acceleration
  - Cache poster, không cache video trong danh sách

## Hiệu Ứng & Tương Tác
- Tải dữ liệu: skeleton shimmer cho media + 2 dòng text
- Animation cho hình ảnh từ trạng thái loading -> có data (nếu có)
- Animation mở tới trang chi tiết sản phẩm khi nhấn.
- Animation debounce khi nhấn vào nút `Cart`
- Cuộn: 60fps, danh sách lazy/virtualized, tránh layout thrash.

## Định Dạng Giá & Số Liệu
- Giá VND: phân cách hàng nghìn, không phần thập phân (vd: `685.000đ`).
- Giảm giá:
  - Có `oldPrice`: strikethrough
  - Có `discountPercent`: chip “‑x%”
  - Có `currentPrice`: “x₫”
- Đã bán: `>=1.000` → `1.0k`, `>=1.000.000` → `1.0M`.
- Đánh giá:
  - Từ 1 - 5 sao
  - 1, 2, 3, 4, 5 hiển thị số ngôi sao nguyên
  - số thập phân hiển thị số sao nguyên + 1 ngôi sao nửa (vd: 4.3 hiển thị 4 ngôi sao + 1 ngôi sao nửa)
