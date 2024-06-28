### Cơ Bản về React
1. **React là gì?**
   - React là một thư viện JavaScript được sử dụng để xây dựng giao diện người dùng, phát triển bởi Facebook. Nó cho phép tạo ra các component tái sử dụng và quản lý state một cách hiệu quả.

2. **Tại sao nên sử dụng React?**
   - Dễ học và sử dụng
   - Tái sử dụng component
   - Hiệu suất cao nhờ Virtual DOM
   - Cộng đồng lớn và hỗ trợ tốt

3. **Virtual DOM là gì?**
   - Virtual DOM là một bản sao nhẹ của DOM thật, giúp tăng tốc độ cập nhật giao diện bằng cách chỉ render lại những phần thay đổi thay vì toàn bộ cây DOM.

4. **JSX là gì?**
   - JSX (JavaScript XML) là cú pháp mở rộng của JavaScript cho phép viết HTML trong JavaScript. JSX được biên dịch thành các lệnh gọi hàm React.createElement().

5. **Component trong React là gì?**
   - Component là khối xây dựng cơ bản của ứng dụng React. Mỗi component đại diện cho một phần giao diện và có thể chứa logic và state riêng.

6. **State là gì?**
   - State là một đối tượng lưu trữ dữ liệu hoặc thông tin về component. Khi state thay đổi, component sẽ re-render để phản ánh sự thay đổi đó.

7. **Props là gì?**
   - Props (properties) là các tham số được truyền từ component cha xuống component con để component con có thể sử dụng chúng.

8. **Làm sao để khởi tạo state trong React?**
   - Trong class component, sử dụng this.state để khởi tạo state.
   - Trong functional component, sử dụng hook useState để khởi tạo state.

9. **Lifecycle của component là gì?**
   - Lifecycle của component là các giai đoạn khác nhau trong vòng đời của một component, bao gồm: Mounting, Updating, và Unmounting.

10. **React Hooks là gì?**
    - React Hooks là các hàm đặc biệt cho phép sử dụng state và các tính năng khác của React trong functional component.

### Cấu Trúc Dự Án và Quản Lý State
11. **Cấu trúc thư mục dự án React thường như thế nào?**
    - src/
      - components/
      - containers/
      - services/
      - utils/
      - App.js
      - index.js

12. **Cách khởi tạo dự án React bằng Create React App?**
    - Chạy lệnh `npx create-react-app tên-dự-án` trong terminal.

13. **Redux là gì?**
    - Redux là một thư viện quản lý state cho các ứng dụng JavaScript, giúp quản lý state một cách dễ dàng và có thể dự đoán được.

14. **useState Hook là gì?**
    - useState là một hook cho phép bạn thêm state vào functional component. Nó trả về một mảng với hai phần tử: giá trị state hiện tại và hàm để cập nhật giá trị đó.

15. **useEffect Hook là gì?**
    - useEffect là một hook cho phép thực hiện các side effect trong functional component, tương tự như các phương thức lifecycle trong class component.

16. **Cách truyền props từ component cha xuống component con?**
    - Sử dụng cú pháp `<ComponentCon propName={value} />` trong component cha để truyền props xuống component con.

17. **Cách cập nhật state trong React?**
    - Trong class component, sử dụng `this.setState({ key: value })`.
    - Trong functional component, sử dụng hàm cập nhật state từ useState, ví dụ: `setState(value)`.

18. **Context API là gì?**
    - Context API cho phép truyền dữ liệu qua các component mà không cần phải truyền props thủ công qua từng cấp.

19. **useContext Hook là gì?**
    - useContext là một hook cho phép bạn sử dụng giá trị context trong functional component.

20. **Redux Thunk là gì?**
    - Redux Thunk là một middleware cho phép bạn viết các action creator trả về một hàm thay vì một action, giúp xử lý logic bất đồng bộ.

### JSX và Render
21. **Cách sử dụng biểu thức JavaScript trong JSX?**
    - Đặt biểu thức JavaScript trong dấu ngoặc nhọn `{}` bên trong JSX, ví dụ: `<h1>{title}</h1>`.

22. **Cách render một danh sách trong React?**
    - Sử dụng phương thức `.map()` để lặp qua mảng và trả về các phần tử JSX, ví dụ: `{items.map(item => <li key={item.id}>{item.name}</li>)}`.

23. **Cách thêm class CSS động vào element trong JSX?**
    - Sử dụng biểu thức trong thuộc tính `className`, ví dụ: `<div className={isActive ? 'active' : ''}></div>`.

24. **Cách render có điều kiện trong React?**
    - Sử dụng toán tử điều kiện (ternary) hoặc toán tử logic để render có điều kiện, ví dụ: `{isLoggedIn ? <LogoutButton /> : <LoginButton />}`.

25. **Fragment là gì?**
    - Fragment là một component đặc biệt cho phép gói các phần tử con mà không thêm node DOM bổ sung.

26. **Cách sử dụng Fragment trong JSX?**
    - Sử dụng `<React.Fragment>` hoặc thẻ rỗng `<> </>` để bao bọc các phần tử con.

27. **Cách gán style trực tiếp trong JSX?**
    - Sử dụng thuộc tính `style` với một đối tượng JavaScript, ví dụ: `<div style={{ color: 'red', fontSize: '20px' }}></div>`.

28. **Cách sử dụng CSS Modules trong React?**
    - Import file CSS module và sử dụng như một đối tượng, ví dụ: `import styles from './Button.module.css';` và `<button className={styles.primary}>Click me</button>`.

29. **Sự khác biệt giữa class component và functional component là gì?**
    - Class component sử dụng cú pháp class và có thể sử dụng state và lifecycle methods.
    - Functional component là các hàm và sử dụng hooks để quản lý state và lifecycle.

30. **Cách sử dụng default props trong React?**
    - Đặt thuộc tính `defaultProps` trên component, ví dụ: `MyComponent.defaultProps = { title: 'Default Title' };`.

### Quản Lý State Nâng Cao
31. **Redux Saga là gì?**
    - Redux Saga là một middleware cho phép quản lý side effects (như gọi API) trong Redux bằng cách sử dụng generator functions.

32. **Cách kết nối Redux với component React?**
    - Sử dụng hàm `connect` từ `react-redux` để kết nối component với store Redux.

33. **Cách chia sẻ state giữa các component không cùng cấp?**
    - Sử dụng Context API hoặc một thư viện quản lý state như Redux hoặc Recoil.

34. **HOC (Higher-Order Component) là gì?**
    - Higher-Order Component là một hàm nhận một component và trả về một component mới với các tính năng bổ sung.

35. **Render props là gì?**
    - Render props là một kỹ thuật cho phép chia sẻ code giữa các component bằng cách sử dụng một prop có giá trị là một hàm để render.

36. **Recoil là gì?**
    - Recoil là một thư viện quản lý state cho React, cung cấp một API đơn giản và hiệu quả cho state management.

37. **React Query là gì?**
    - React Query là một thư viện cho phép quản lý state bất đồng bộ trong React, đặc biệt là quản lý dữ liệu từ server.

38. **Cách tạo custom hooks trong React?**
    - Viết một hàm sử dụng các hook khác và trả về giá trị hoặc hàm cần thiết, ví dụ:
    ```javascript
    function useCustomHook() {
      const [state, setState] = useState(initialState);
      // logic tùy chỉnh
      return [state, setState];
    }
    ```

39. **Sự khác biệt giữa useEffect và useLayoutEffect là gì?**
    - `useEffect` chạy sau khi render hoàn tất.
    - `useLayoutEffect` chạy trước khi browser vẽ màn hình, đảm bảo DOM đã cập nhật.

40. **Sự khác biệt giữa useState và useReducer là gì?**
    - `useState` dùng để quản lý state đơn giản.
    - `useReducer` dùng để quản lý state phức tạp với nhiều logic cập nhật state.

### Quản Lý Hiệu Năng và Tối Ưu
41. **React.memo là gì?**
    - `React.memo` là một HOC giúp tối ưu hóa performance bằng cách ghi nhớ kết quả render của component và chỉ re-render nếu props thay đổi.

42. **useCallback Hook là gì?**
    - `useCallback` là một hook trả về phiên bản ghi nhớ của hàm callback, giúp tránh tạo lại hàm không cần thiết mỗi khi component re-render.

43. **useMemo Hook là gì?**
    - `useMemo` là một hook trả về giá trị đã ghi nhớ của một biểu thức, giúp tối ưu hóa việc tính toán lại giá trị không cần thiết mỗi khi component re-render.

44. **Cách tối ưu hóa render trong React?**
    - Sử dụng React.memo, useCallback, useMemo, và kỹ thuật code splitting.

45. **Lazy Loading là gì?**
    - Lazy Loading là kỹ thuật chỉ tải các thành phần cần thiết khi chúng thực sự được yêu cầu, giúp giảm thời gian tải trang ban đầu.

46. **Cách sử dụng React.lazy và Suspense để lazy load component?**
    - Sử dụng `React.lazy` để load component và bọc component bằng `Suspense` với fallback component.
    ```javascript
    const LazyComponent = React.lazy(() => import('./LazyComponent'));
    <Suspense fallback={<div>Loading...</div>}>
      <LazyComponent />
    </Suspense>
    ```

47. **Code Splitting là gì?**
    - Code Splitting là kỹ thuật chia nhỏ bundle JavaScript thành nhiều phần nhỏ để tải từng phần khi cần thiết, giúp cải thiện hiệu suất.

48. **React DevTools là gì?**
    - React DevTools là một tiện ích mở rộng cho trình duyệt giúp kiểm tra và gỡ lỗi các ứng dụng React.

49. **Cách đo lường hiệu suất ứng dụng React?**
    - Sử dụng React DevTools, Performance tab của trình duyệt, và các công cụ như Lighthouse.

50. **Cách sử dụng useTransition hook?**
    - `useTransition` là một hook cho phép quản lý các cập nhật state không khẩn cấp, giúp tránh các update không cần thiết ảnh hưởng đến hiệu suất.

### Giao Tiếp với Backend
51. **Cách thực hiện request HTTP trong React?**
    - Sử dụng `fetch` hoặc thư viện `axios` để thực hiện request HTTP.

52. **Cách xử lý dữ liệu bất đồng bộ trong React?**
    - Sử dụng các hook như `useEffect` để xử lý các request bất đồng bộ và cập nhật state khi dữ liệu đã được fetch.

53. **Cách sử dụng React Query để quản lý request HTTP?**
    - Sử dụng hook `useQuery` và `useMutation` từ React Query để quản lý request HTTP và caching dữ liệu.

54. **Cách kết hợp GraphQL với React?**
    - Sử dụng thư viện `Apollo Client` hoặc `Relay` để kết hợp GraphQL với React.

55. **Cách bảo mật các request HTTP trong React?**
    - Sử dụng HTTPS, token-based authentication (JWT), và các biện pháp bảo mật khác để bảo vệ request HTTP.

56. **Sự khác biệt giữa REST API và GraphQL là gì?**
    - REST API sử dụng các endpoint cụ thể cho từng resource, trong khi GraphQL sử dụng một endpoint duy nhất và cho phép client yêu cầu chính xác dữ liệu cần thiết.

57. **Cách xử lý lỗi khi thực hiện request HTTP?**
    - Sử dụng `try-catch` hoặc phương thức `.catch()` để xử lý lỗi khi thực hiện request HTTP và hiển thị thông báo lỗi cho người dùng.

58. **CORS là gì và cách xử lý lỗi CORS trong React?**
    - CORS (Cross-Origin Resource Sharing) là một chính sách bảo mật ngăn chặn việc request tài nguyên từ domain khác. Để xử lý lỗi CORS, cần cấu hình server để cho phép các request từ domain của bạn.

59. **Cách xử lý loading state trong React khi fetch data?**
    - Sử dụng state để quản lý loading state và hiển thị spinner hoặc thông báo khi dữ liệu đang được fetch.

60. **Cách quản lý state bất đồng bộ trong React?**
    - Sử dụng các hook như `useState`, `useEffect`, và `useReducer` để quản lý state bất đồng bộ, hoặc sử dụng thư viện như React Query hoặc Redux Thunk.

### Form và Validation
61. **Cách tạo form trong React?**
    - Sử dụng các thẻ HTML như `<form>`, `<input>`, `<textarea>`, và `<button>` để tạo form.

62. **Cách quản lý state của form trong React?**
    - Sử dụng hook `useState` để quản lý state của các input field trong form.

63. **Cách xử lý sự kiện form submit trong React?**
    - Sử dụng thuộc tính `onSubmit` của thẻ `<form>` và ngăn chặn hành vi mặc định bằng `event.preventDefault()`.

64. **Cách validate dữ liệu form trong React?**
    - Sử dụng các hàm validation tùy chỉnh hoặc thư viện như Yup để validate dữ liệu form trước khi submit.

65. **Thư viện nào có thể dùng để validate form trong React?**
    - Một số thư viện phổ biến để validate form trong React là Formik và React Hook Form.

66. **Cách sử dụng thư viện Formik trong React?**
    - Import Formik và các component liên quan, sau đó sử dụng chúng để tạo và quản lý form.
    ```javascript
    import { Formik, Form, Field } from 'formik';
    <Formik initialValues={{ name: '' }} onSubmit={values => console.log(values)}>
      <Form>
        <Field name="name" />
        <button type="submit">Submit</button>
      </Form>
    </Formik>
    ```

67. **Cách sử dụng thư viện React Hook Form?**
    - Import các hook từ React Hook Form và sử dụng chúng để tạo và quản lý form.
    ```javascript
    import { useForm } from 'react-hook-form';
    const { register, handleSubmit } = useForm();
    <form onSubmit={handleSubmit(onSubmit)}>
      <input {...register('name')} />
      <button type="submit">Submit</button>
    </form>
    ```

68. **Cách tích hợp form với Redux?**
    - Sử dụng thư viện redux-form để kết hợp form với Redux, giúp quản lý state của form trong store Redux.

69. **Cách hiển thị lỗi validation trong form?**
    - Sử dụng state hoặc các thuộc tính của thư viện form để lưu trữ và hiển thị thông báo lỗi cho từng input field.

70. **Cách tạo các thành phần form tùy chỉnh trong React?**
    - Tạo các component riêng cho từng thành phần form và sử dụng chúng trong form chính, ví dụ: `CustomInput`, `CustomSelect`.

### Routing
71. **React Router là gì?**
    - React Router là một thư viện giúp quản lý routing trong ứng dụng React, cho phép điều hướng giữa các trang mà không cần tải lại trang.

72. **Cách cài đặt React Router?**
    - Chạy lệnh `npm install react-router-dom` để cài đặt React Router.

73. **Cách tạo route trong React?**
    - Sử dụng các component `BrowserRouter`, `Route`, và `Switch` từ react-router-dom để định nghĩa các route.
    ```javascript
    import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';
    <Router>
      <Switch>
        <Route path="/" exact component={Home} />
        <Route path="/about" component={About} />
      </Switch>
    </Router>
    ```

74. **Cách sử dụng Link component trong React Router?**
    - Sử dụng component `Link` từ react-router-dom để tạo các liên kết điều hướng.
    ```javascript
    import { Link } from 'react-router-dom';
    <Link to="/about">About</Link>
    ```

75. **Cách sử dụng useParams hook trong React Router?**
    - Sử dụng hook `useParams` để truy cập các tham số động từ URL.
    ```javascript
    import { useParams } from 'react-router-dom';
    const { id } = useParams();
    ```

76. **Cách sử dụng useHistory hook trong React Router?**
    - Sử dụng hook `useHistory` để truy cập lịch sử điều hướng và thực hiện các hành động như push hoặc goBack.
    ```javascript
    import { useHistory } from 'react-router-dom';
    const history = useHistory();
    history.push('/new-path');
    ```

77. **Cách tạo nested routes trong React?**
    - Sử dụng các component `Route` bên trong các component khác để tạo nested routes.
    ```javascript
    <Route path="/dashboard" component={Dashboard}>
      <Route path="/dashboard/stats" component={Stats} />
    </Route>
    ```

78. **Cách bảo vệ route với authentication trong React Router?**
    - Tạo một component bảo vệ (ProtectedRoute) và sử dụng logic kiểm tra authentication để render component thích hợp.
    ```javascript
    const ProtectedRoute = ({ component: Component, ...rest }) => (
      <Route {...rest} render={(props) => (
        isAuthenticated ? <Component {...props} /> : <Redirect to="/login" />
      )} />
    );
    ```

79. **Cách xử lý redirect trong React Router?**
    - Sử dụng component `Redirect` hoặc phương thức `history.push` để thực hiện redirect.
    ```javascript
    import { Redirect } from 'react-router-dom';
    <Redirect to="/new-path" />
    ```

80. **Cách tạo trang 404 tùy chỉnh trong React Router?**
    - Định nghĩa một route không có path hoặc sử dụng dấu `*` để bắt tất cả các route không khớp.
    ```javascript
    <Route path="*" component={NotFound} />
    ```

### Testing
81. **Cách viết test cho component React?**
    - Sử dụng các thư viện như Jest và React Testing Library để viết các bài test cho component.

82. **Jest là gì và cách sử dụng Jest trong React?**
    - Jest là một framework test JavaScript được sử dụng để viết các bài test cho ứng dụng React. Bạn có thể chạy các test bằng cách sử dụng lệnh `npm test`.

83. **Enzyme là gì và cách sử dụng Enzyme trong React?**
    - Enzyme là một thư viện test cho React, cung cấp các phương thức để render, tìm kiếm, và tương tác với các component React.

84. **Sự khác biệt giữa shallow rendering và full rendering trong Enzyme là gì?**
    - Shallow rendering chỉ render component hiện tại mà không render các component con.
    - Full rendering (mount) render toàn bộ cây component, bao gồm các component con.

85. **Cách viết snapshot test trong React?**
    - Sử dụng Jest và React Test Renderer để tạo snapshot test, so sánh đầu ra hiện tại của component với snapshot trước đó.
    ```javascript
    import renderer from 'react-test-renderer';
    const tree = renderer.create(<MyComponent />).toJSON();
    expect(tree).toMatchSnapshot();
    ```

86. **Cách test event handler trong React?**
    - Sử dụng React Testing Library hoặc Enzyme để mô phỏng các sự kiện và kiểm tra kết quả.
    ```javascript
    fireEvent.click(button);
    expect(handleClick).toHaveBeenCalled();
    ```

87. **Cách test async component trong React?**
    - Sử dụng `waitFor` hoặc `findBy` từ React Testing Library để chờ các cập nhật async.
    ```javascript
    await waitFor(() => expect(getByText('Async Text')).toBeInTheDocument());
    ```

88. **Cách sử dụng React Testing Library?**
    - Sử dụng các hàm từ React Testing Library để render component và kiểm tra đầu ra.
    ```javascript
    import { render, screen } from '@testing-library/react';
    render(<MyComponent />);
    expect(screen.getByText('Hello')).toBeInTheDocument();
    ```

89. **Cách mô phỏng props trong test?**
    - Truyền các props giả lập vào component khi render trong bài test.
    ```javascript
    render(<MyComponent prop1="value1" />);
    ```

90. **Cách viết unit test cho custom hooks trong React?**
    - Sử dụng thư viện `@testing-library/react-hooks` để render và kiểm tra custom hooks.
    ```javascript
    import { renderHook } from '@testing-library/react-hooks';
    const { result } = renderHook(() => useCustomHook());
    expect(result.current).toBe(expectedValue);
    ```

### Khác
91. **React Portal là gì?**
    - React Portal cho phép render các phần tử con vào một DOM node khác bên ngoài của DOM hierarchy hiện tại của component.

92. **Cách sử dụng React Portal?**
    - Sử dụng `ReactDOM.createPortal` để render phần tử con vào node khác.
    ```javascript
    import ReactDOM from 'react-dom';
    ReactDOM.createPortal(<ChildComponent />, document.getElementById('portal-root'));
    ```

93. **Cách quản lý modal trong React?**
    - Sử dụng state để quản lý hiển thị modal và React Portal để render modal ra ngoài cây DOM chính.
    ```javascript
    const [isOpen, setIsOpen] = useState(false);
    isOpen && ReactDOM.createPortal(<Modal />, document.getElementById('modal-root'));
    ```

94. **Cách tạo component có thể tái sử dụng trong React?**
    - Thiết kế component có các props linh hoạt và không phụ thuộc vào ngữ cảnh cụ thể.

95. **Sự khác biệt giữa controlled và uncontrolled components là gì?**
    - Controlled component có giá trị state được quản lý bởi React thông qua props.
    - Uncontrolled component có giá trị state được quản lý bởi DOM thông qua refs.

96. **Cách sử dụng forwardRef trong React?**
    - Sử dụng `React.forwardRef` để chuyển tiếp ref từ component cha xuống component con.
    ```javascript
    const MyComponent = React.forwardRef((props, ref) => (
      <input ref={ref} {...props} />
    ));
    ```

97. **Cách quản lý focus trong form?**
    - Sử dụng refs để quản lý focus của các input field trong form.
    ```javascript
    const inputRef = useRef();
    useEffect(() => {
      inputRef.current.focus();
    }, []);
    ```

98. **Cách xử lý animation trong React?**
    - Sử dụng CSS animations, libraries như `react-transition-group`, hoặc `framer-motion` để thêm animation vào component React.

99. **Cách tích hợp React với TypeScript?**
    - Đổi phần mở rộng file từ `.js` sang `.tsx` và cài đặt TypeScript cùng các typings cho React.
    ```bash
    npm install typescript @types/react @types/react-dom
    ```

100. **Cách deploy ứng dụng React lên server?**
    - Build ứng dụng bằng cách chạy `npm run build` và deploy thư mục build lên server hoặc dịch vụ hosting như Netlify, Vercel, hoặc Heroku.
