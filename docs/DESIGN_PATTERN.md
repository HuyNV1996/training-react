## Các Design Pattern trong React

### 1. Component-Based Architecture

- **Định nghĩa**: Xây dựng ứng dụng dựa trên các component độc lập, mỗi component chịu trách nhiệm hiển thị giao diện và xử lý logic riêng biệt.

- **Lợi ích**: Tái sử dụng mã nguồn, dễ bảo trì và mở rộng ứng dụng.

### 2. Container-Presentational Components

- **Định nghĩa**: Phân tách các component thành hai loại: Container components (quản lý state và logic) và Presentational components (hiển thị UI).

- **Lợi ích**: Tăng khả năng tái sử dụng, rõ ràng hóa luồng dữ liệu và logic.

### 3. Higher-Order Components (HOC)

- **Định nghĩa**: HOC là một hàm nhận component làm đối số và trả về một component mới.

- **Lợi ích**: Tái sử dụng logic chung, chia sẻ state và props một cách hiệu quả giữa các component.

### 4. Render Props

- **Định nghĩa**: Truyền một prop là một hàm từ một component cha xuống component con để chia sẻ logic render.

- **Lợi ích**: Tái sử dụng logic render một cách linh hoạt, giúp tăng khả năng tái sử dụng và bảo trì.

### 5. Redux (State Management)

- **Định nghĩa**: Quản lý trạng thái ứng dụng trong một store duy nhất và truy cập trạng thái thông qua các reducers.

- **Lợi ích**: Quản lý trạng thái toàn cục, dễ dàng theo dõi và thay đổi trạng thái ứng dụng.

### 6. Context API

- **Định nghĩa**: Cung cấp một cách để truyền dữ liệu qua nhiều cấp độ component mà không cần truyền props thủ công từng bước.

- **Lợi ích**: Giảm sự phụ thuộc vào props, giúp quản lý dữ liệu toàn cục một cách hiệu quả.

### 7. Error Boundary

- **Định nghĩa**: Component dùng để bao bọc các component con và bắt lỗi xảy ra trong chúng.

- **Lợi ích**: Ngăn chặn lỗi lan rộng, cải thiện trải nghiệm người dùng.

### 8. Lazy Loading

- **Định nghĩa**: Tải các phần của ứng dụng khi cần thiết thay vì tải toàn bộ ứng dụng từ đầu.

- **Lợi ích**: Tăng tốc độ tải trang và giảm tải cho máy chủ.

### 9. Code Splitting

- **Định nghĩa**: Chia ứng dụng thành các chunk nhỏ hơn để tải một cách hiệu quả và linh hoạt.

- **Lợi ích**: Giảm thời gian tải ban đầu và tối ưu hóa hiệu suất ứng dụng.

### 10. Hooks

- **Định nghĩa**: Là các hàm đặc biệt trong React cho phép bạn sử dụng state và các tính năng React khác trong functional components.

- **Lợi ích**: Giúp tái sử dụng logic và state trong functional components một cách dễ dàng.

Các design pattern này giúp bạn tổ chức mã nguồn React một cách hợp lý và hiệu quả, giảm thiểu lặp lại và tối ưu hóa hiệu suất của ứng dụng.
