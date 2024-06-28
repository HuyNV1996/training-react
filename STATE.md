### Câu hỏi và trả lời về Quản lý State trong React

#### Cơ Bản về State

1. **State trong React là gì?**
   - State trong React là một đối tượng chứa dữ liệu hoặc thông tin về component. Nó có thể thay đổi theo thời gian và khi state thay đổi, component sẽ re-render để phản ánh sự thay đổi đó.

2. **Làm sao để khởi tạo state trong React?**
   - Trong class component:
     ```javascript
     class MyComponent extends React.Component {
       constructor(props) {
         super(props);
         this.state = { count: 0 };
       }
     }
     ```
   - Trong functional component:
     ```javascript
     const [count, setCount] = useState(0);
     ```

3. **Làm thế nào để cập nhật state trong React?**
   - Trong class component:
     ```javascript
     this.setState({ count: this.state.count + 1 });
     ```
   - Trong functional component:
     ```javascript
     setCount(count + 1);
     ```

#### Quản Lý State trong Functional Component

4. **React Hooks là gì?**
   - React Hooks là các hàm đặc biệt trong React cho phép sử dụng state và các tính năng khác của React trong functional components. Các hook phổ biến bao gồm `useState`, `useEffect`, `useContext`, `useReducer`.

5. **useState Hook là gì?**
   - `useState` là một hook cho phép thêm state vào functional component. Nó trả về một mảng gồm hai phần tử: giá trị state hiện tại và một hàm để cập nhật state đó.

6. **useReducer Hook là gì?**
   - `useReducer` là một hook cho phép quản lý state phức tạp hơn sử dụng reducer function. Nó trả về state hiện tại và một dispatch function để gửi các action.

#### Quản Lý State Toàn Cục

7. **Context API là gì?**
   - Context API là một tính năng trong React cho phép truyền dữ liệu qua cây component mà không cần phải truyền props xuống từng cấp.

8. **Làm sao để sử dụng Context API?**
   - Tạo context:
     ```javascript
     const MyContext = React.createContext();
     ```
   - Sử dụng Provider để cung cấp dữ liệu:
     ```javascript
     <MyContext.Provider value={/* some value */}>
       <MyComponent />
     </MyContext.Provider>
     ```
   - Sử dụng Consumer hoặc `useContext` để truy cập dữ liệu:
     ```javascript
     const value = useContext(MyContext);
     ```

9. **Redux là gì?**
   - Redux là một thư viện quản lý state cho các ứng dụng JavaScript. Nó giúp quản lý state toàn cục của ứng dụng trong một store duy nhất.

10. **Làm thế nào để kết nối Redux với component React?**
    - Sử dụng `Provider` từ `react-redux` để cung cấp store cho ứng dụng:
      ```javascript
      import { Provider } from 'react-redux';
      import { createStore } from 'redux';

      const store = createStore(reducer);

      <Provider store={store}>
        <App />
      </Provider>
      ```
    - Sử dụng `useSelector` để truy cập state từ store và `useDispatch` để gửi action:
      ```javascript
      const count = useSelector((state) => state.count);
      const dispatch = useDispatch();
      dispatch({ type: 'INCREMENT' });
      ```

#### Nâng Cao

11. **Redux Thunk là gì?**
    - Redux Thunk là một middleware cho phép viết các action creators trả về một hàm thay vì một đối tượng. Điều này hữu ích cho các hành động bất đồng bộ như gọi API.

12. **Làm thế nào để sử dụng Redux Thunk?**
    - Cài đặt redux-thunk và thêm vào middleware:
      ```javascript
      import thunk from 'redux-thunk';
      const store = createStore(reducer, applyMiddleware(thunk));
      ```
    - Viết một action creator bất đồng bộ:
      ```javascript
      const fetchData = () => {
        return async (dispatch) => {
          const response = await fetch('/api/data');
          const data = await response.json();
          dispatch({ type: 'FETCH_DATA_SUCCESS', payload: data });
        };
      };
      ```

13. **Recoil là gì?**
    - Recoil là một thư viện quản lý state cho React cung cấp một cách tiếp cận mới để quản lý state với atoms và selectors.

14. **Làm thế nào để sử dụng Recoil?**
    - Cài đặt recoil và thêm `RecoilRoot` vào cây component:
      ```javascript
      import { RecoilRoot } from 'recoil';

      <RecoilRoot>
        <App />
      </RecoilRoot>
      ```
    - Tạo atom để lưu trữ state:
      ```javascript
      import { atom, useRecoilState } from 'recoil';

      const countState = atom({
        key: 'countState',
        default: 0,
      });

      const Component = () => {
        const [count, setCount] = useRecoilState(countState);
      };
      ```

15. **useContext Hook là gì?**
    - `useContext` là một hook cho phép truy cập vào giá trị của một context trực tiếp trong functional component. Nó nhận vào một context object và trả về giá trị hiện tại của context đó.
