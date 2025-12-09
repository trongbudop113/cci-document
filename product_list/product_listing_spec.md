# Product Listing — Generate UI Spec

**Date:** 07/12/2025  
**Version:** 1.0  
**Description:** Thêm mới  
**Author:** IT Team  

## Mục Tiêu

Chuẩn hoá tài liệu để Generate UI/UX, giúp AI tool hiểu và sinh code hiển thị danh sách sản phẩm đúng theo design.

Định nghĩa rõ:

- Loại item
- Thuật ngữ layout
- Quy tắc hiển thị ảnh/video
- Hiệu ứng
- Cấu trúc dữ liệu

Mục tiêu: đảm bảo UI/logic nhất quán cho các block danh sách sản phẩm.

## Phạm Vi Áp Dụng

- Màn hình danh sách sản phẩm dạng **lưới 2 cột**  
- Có thể xen kẽ **banner toàn chiều ngang** và **thẻ nội dung** (editorial/review)  
- Nền tảng: **App**

## Thuật Ngữ Khoảng Cách & Kích Thước

### Đơn vị
- **px**: khoảng cách  
- **sp**: kích thước chữ  

### Thuật ngữ chung
- **margin:** khoảng cách bên ngoài phần tử  
- **padding:** khoảng cách bên trong  
- **line-spacing:** khoảng cách giữa các dòng  
- **gap:** khoảng cách giữa các component  
- **border-radius:** bo góc  
- **font-size:** kích thước chữ  
- **font-weight:** độ dày chữ  
- **max-line:** số dòng tối đa

## Loại Item Hiển Thị

### News

### Banner quảng cáo dạng slide

### Sản phẩm

| STT | Loại sản phẩm | Hình minh họa |
|-----|----------------|---------------|
| 1 | Sản phẩm thường | ![alt text](http://url/to/img.png) |
| 2 | Sản phẩm giảm giá | |
| 3 | Sản phẩm kèm quà tặng | |
| 4 | Sản phẩm kèm quà tặng và giảm giá | |
| 5 | Sản phẩm khuyến mãi đơn hàng | |

## Thành Phần Mỗi Product Item

### Khoảng cách & kích thước
- **margin:** 5px  
- **padding:** 6px  
- **font-size:**  
  - title: 13sp  
  - oldPrice: 12sp  
  - currentPrice: 16sp  
- **line-spacing:** 16 / 13  
- **gap:**  
  - ảnh → title: 6px  
  - title → rating: 12px  
  - rating → price: 12px

### Media
- Ảnh/video **tỉ lệ 1:1**

### Label
- Ví dụ: `"FREESHIP"`, `"siêu tốc 1h"`.

### Frame khuyến mãi
- Khung chương trình khuyến mãi

### Tiêu đề
- Tối đa **2 dòng**
- Tràn: hiển thị **ellipsis (…)**

### Thông tin phụ
- Brand/cửa hàng/khoảng cách giao  
- Tối đa **1 dòng**

### Giá
- **oldPrice**: tùy chọn (gạch ngang)  
- **discountPercent / discountValue**: nếu có  
- **currentPrice**: luôn có  

### Rating & đã bán
- Đánh giá: **1–5 sao**  
- “Đã bán x” format rút gọn → *1.2k, 2.4k+*

### Badge giỏ hàng
- Hiển thị khi sản phẩm đã được thêm  
- Vị trí: góc phải nút “Thêm vào giỏ”  
- font-size: 11sp  
- background: **#FF6400**  
- border-radius: 10px  

### Background khuyến mãi đơn hàng

### Hành động
- Thêm vào giỏ  
- Xem chi tiết  

## Xử Lý Ảnh Sản Phẩm

### Tỉ lệ hiển thị
- Khung 1:1  
- Nếu **height = width** → fit toàn khung  
- Nếu **height > width** → fit theo height  
- Nếu **height < width** → fit theo width  

### Placeholder
- Khi tải: nền xám + **shimmer**  
- Khi lỗi: logo ConCung giữa nền trắng  

### Tối ưu hóa
- **Prefetch** khi vào gần viewport  
- **Cache** theo id/url + kích thước khung  

## Xử Lý Video

- **Poster:** ảnh tĩnh + icon play  
- **Auto-play:** tắt trong danh sách  
- Play khi **người dùng nhấn**  
- Khi phát inline:  
  - Mute mặc định  
  - Pause khi rời viewport hoặc cuộn  

### Tài nguyên
- Player native  
- Hardware acceleration  
- Cache poster  
- Không cache video trong danh sách  

## Hiệu Ứng & Tương Tác

- Skeleton shimmer cho media + text  
- Animation từ loading → có data  
- Animation mở trang chi tiết  
- Debounce khi nhấn nút cart  
- Cuộn 60fps  
- Danh sách lazy / virtualized  
- Tránh layout thrashing  

## Định Dạng Giá & Số Liệu

### Giá VND
- Phân cách hàng nghìn  
- Không thập phân  
- Ví dụ: `685.000đ`

### Giảm giá
- Có **oldPrice** → gạch ngang  
- Có **discountPercent** → chip “-x%”  
- Có **currentPrice** → “x₫”

### Đã bán
- >= 1,000 → `1.0k`  
- >= 1,000,000 → `1.0M`
