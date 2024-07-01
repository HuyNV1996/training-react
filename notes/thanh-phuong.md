# Context API, React query, React Redux
## 1.  Context API
- Mục đích : Được sử dụng để truyền dữ liệu qua các component mà không cần phải truyền props theo cấp bậc. Quản lý state trong phạm vi nhỏ hoặc trung bình, đặc biệt là khi không có yêu cầu phức tạp về quản lý state.
- Ví dụ:
```
import React, { createContext, useContext, useState } from 'react';

const MyContext = createContext();

const MyProvider = ({ children }) => {
  const [state, setState] = useState("Hello World");

  return (
    <MyContext.Provider value={{ state, setState }}>
      {children}
    </MyContext.Provider>
  );
};

const MyComponent = () => {
  const { state, setState } = useContext(MyContext);

  return (
    <div>
      <p>{state}</p>
      <button onClick={() => setState("Hello React")}>Change Text</button>
    </div>
  );
};

export default function App() {
  return (
    <MyProvider>
      <MyComponent />
    </MyProvider>
  );
}
```
## 2. React query
- Mục đích: Quản lý dữ liệu truy vấn từ API và caching dữ liệu đó một cách hiệu quả.
- Ví dụ:
```
import React from 'react';
import { useQuery } from 'react-query';

const fetchPosts = async () => {
  const response = await fetch('https://jsonplaceholder.typicode.com/posts');
  return response.json();
};

const Posts = () => {
  const { data, error, isLoading } = useQuery('posts', fetchPosts); //posts: key của truy vấn. Key này dùng để định danh truy vấn và quản lý caching.

  if (isLoading) return <span>Loading...</span>;
  if (error) return <span>Error: {error.message}</span>;

  return (
    <div>
      {data.map(post => (
        <div key={post.id}>
          <h3>{post.title}</h3>
          <p>{post.body}</p>
        </div>
      ))}
    </div>
  );
};

export default Posts;
```
## 3. React Redux
- Mục dích: Quản lý state toàn cục cho các ứng dụng lớn và phức tạp.
- Ví dụ:
```
import React from 'react';
import { createStore } from 'redux';
import { Provider, useDispatch, useSelector } from 'react-redux';

// Actions: các đối tượng mô tả những thay đổi có thể xảy ra trong ứng dụng.
const INCREMENT = 'INCREMENT';

const increment = () => ({
  type: INCREMENT
});

// Reducer: hàm xác định cách state của ứng dụng thay đổi để phản ứng lại các actions.
const initialState = { count: 0 };

const counterReducer = (state = initialState, action) => {
  switch (action.type) {
    case INCREMENT:
      return { count: state.count + 1 };
    default:
      return state;
  }
};

// Store: chứa toàn bộ state của ứng dụng và cung cấp các phương thức để truy cập, cập nhật state và đăng ký các listener.
const store = createStore(counterReducer);

const Counter = () => {
  const count = useSelector(state => state.count);
  const dispatch = useDispatch();

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => dispatch(increment())}>Increment</button>
    </div>
  );
};

export default function App() {
  return (
    <Provider store={store}>
      <Counter />
    </Provider>
  );
}
```

## Bảng so sánh tổng quan

## Table
| Công cụ | Mục đích | Ưu điểm | Nhược điểm | Sử dụng khi nào |
|-----|-----|-----|-----|-----|
| **Context API** | Quản lý state đơn giản | Đơn giản, không cần thư viện bổ sung  | Không thích hợp cho state phức tạp, gây re-render không cần thiết | Khi cần chia sẻ state đơn giản giữa các component |
| **React Query** | Quản lý dữ liệu truy vấn từ API | Quản lý dữ liệu tự động, caching, refetching | Cần thêm thư viện, có đường cong học tập | Khi cần quản lý dữ liệu từ API hiệu quả |
| **Redux** | Quản lý state toàn cục | Quản lý nhất quán, dễ mở rộng, nhiều công cụ hỗ trợ | Cấu hình phức tạp, quá mức cho ứng dụng đơn giản | Khi cần quản lý state toàn cục cho ứng dụng lớn |


  
