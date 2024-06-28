# Câu hỏi và câu trả lời về Bản chất Render của React

1. **Render trong React là gì?**
   - Render là quá trình tạo ra cây DOM ảo từ các component React dựa trên trạng thái (state) và thuộc tính (props).

2. **Virtual DOM là gì và vai trò của nó trong quá trình render của React là gì?**
   - Virtual DOM là một biểu diễn trong bộ nhớ của cây DOM thực tế trên trình duyệt. Nó giúp React so sánh và cập nhật DOM hiệu quả hơn.

3. **Sự khác biệt giữa reconciliation và rendering trong React là gì?**
   - Rendering: Quá trình tạo ra cây DOM ảo ban đầu từ các component.
   - Reconciliation: Quá trình so sánh cây DOM ảo mới và cây DOM ảo hiện tại để xác định sự thay đổi và cập nhật DOM thực tế.

4. **React làm thế nào để quản lý và tối ưu hóa quá trình render của các component?**
   - React sử dụng Virtual DOM và thuật toán reconciliation để chỉ cập nhật những phần DOM thực sự thay đổi, giúp tăng hiệu suất render.

5. **Thuật toán Reconciliation trong React hoạt động như thế nào và tại sao nó quan trọng?**
   - Reconciliation là quá trình so sánh từng node trong cây DOM ảo mới và cây DOM ảo cũ để xác định sự thay đổi, giúp React chỉ render lại những phần cần thiết, làm giảm tải cho trình duyệt.

6. **Sự khác biệt giữa React render và re-render là gì?**
   - Render: Quá trình ban đầu tạo giao diện dựa trên state và props.
   - Re-render: Quá trình cập nhật lại giao diện khi state hoặc props thay đổi.

7. **Lifecycle của một component trong quá trình render là gì và có những pha nào?**
   - Lifecycle của component bao gồm các pha: Mounting (khởi tạo), Updating (cập nhật), Unmounting (hủy), và Error Handling (xử lý lỗi).

8. **React làm thế nào để xử lý render một cách bất đồng bộ?**
   - React hỗ trợ xử lý render bất đồng bộ thông qua các phương thức như `setState` và `useEffect`, cho phép thực hiện các tác vụ như fetch data mà không làm gián đoạn UI.

9. **Sự khác biệt giữa client-side render và server-side render trong React là gì?**
   - Client-side render: React tạo và quản lý giao diện trực tiếp trên trình duyệt của người dùng.
   - Server-side render: React tạo và render giao diện trước khi gửi đến trình duyệt, giúp tối ưu hóa thời gian tải trang.

10. **React Hooks và tối ưu hóa quá trình render của functional component như thế nào?**
    - React Hooks như `useState` và `useEffect` giúp functional component có thể sử dụng state và lifecycle như class component, giúp tối ưu hóa và tái sử dụng code.

