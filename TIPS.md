### 1. Debouncing trong React

#### Mô tả

Debouncing là hai kỹ thuật quan trọng để kiểm soát tần suất gọi hàm trong ứng dụng React, đặc biệt là khi xử lý các sự kiện như scroll, resize, hoặc các tương tác người dùng khác.

##### Ví dụ

```javascript
import React, { useState } from 'react';

const DebouncingComponent = () => {
  const [searchTerm, setSearchTerm] = useState('');

  const debounce = (func, delay) => {
    let timer;
    return function (...args) {
      clearTimeout(timer);
      timer = setTimeout(() => {
        func.apply(this, args);
      }, delay);
    };
  };

  const handleSearch = debounce(search => {
    // Call API or perform search logic
    console.log('Searching for:', search);
  }, 500); // Debounce delay: 500ms

  const handleChange = event => {
    const { value } = event.target;
    setSearchTerm(value);
    handleSearch(value);
  };

  return (
    <div>
      <input type="text" value={searchTerm} onChange={handleChange} placeholder="Search..." />
    </div>
  );
};

export default DebouncingComponent;
```
### 2.Memoization trong React

#### Mô tả

Memoization là kỹ thuật tối ưu hóa hiệu suất trong React bằng cách lưu lại kết quả của các hàm để tránh tính toán lại các giá trị đã tính toán trước đó. Điều này giúp giảm thiểu thời gian thực thi và tối ưu hóa render của các component.

#### Ví dụ

```javascript
import React, { useState, useMemo } from 'react';

const MemoizationComponent = () => {
  const [count, setCount] = useState(0);

  // Memoize factorial calculation to avoid recalculating on every render
  const factorial = useMemo(() => {
    console.log('Calculating factorial...');
    let result = 1;
    for (let i = 1; i <= count; i++) {
      result *= i;
    }
    return result;
  }, [count]); // Dependency array: recompute factorial only when count changes

  return (
    <div>
      <p>Count: {count}</p>
      <p>Factorial of {count} is: {factorial}</p>
      <button onClick={() => setCount(count + 1)}>Increment Count</button>
    </div>
  );
};

export default MemoizationComponent;
```
### 3. Sử dụng Async/Await trong React

#### Mô tả

Async/Await là một kỹ thuật xử lý bất đồng bộ trong JavaScript, giúp viết code rõ ràng hơn khi làm việc với các hàm có thao tác mạng, API trong React.

#### Ví dụ

```javascript
import React, { useState } from 'react';

const AsyncAwaitComponent = () => {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(false);

  const fetchData = async () => {
    setLoading(true);
    try {
      const response = await fetch('https://api.example.com/data');
      const result = await response.json();
      setData(result);
    } catch (error) {
      console.error('Error fetching data:', error);
    } finally {
      setLoading(false);
    }
  };

  return (
    <div>
      {loading ? (
        <p>Loading...</p>
      ) : data ? (
        <ul>
          {data.map(item => (
            <li key={item.id}>{item.name}</li>
          ))}
        </ul>
      ) : (
        <button onClick={fetchData}>Fetch Data</button>
      )}
    </div>
  );
};

export default AsyncAwaitComponent;
```
### 4. Memoization trong React

#### Mô tả

Memoization là kỹ thuật lưu lại kết quả của các hàm để tránh tính toán lại các giá trị đã tính toán trước đó, giúp tối ưu hóa hiệu suất của ứng dụng React. Thường được sử dụng để giữ lại kết quả của các hàm số phức tạp, như tính toán dữ liệu từ API.

#### Ví dụ

```javascript
import React, { useState, useMemo } from 'react';

const MemoizedComponent = () => {
  const [count, setCount] = useState(0);

  // Tính toán giai thừa của count bằng useMemo để tránh tính toán lại khi count thay đổi
  const factorial = useMemo(() => {
    console.log('Calculating factorial...');
    let result = 1;
    for (let i = 1; i <= count; i++) {
      result *= i;
    }
    return result;
  }, [count]);

  return (
    <div>
      <p>Count: {count}</p>
      <p>Factorial of {count} is: {factorial}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
};
export default MemoizedComponent;
```
### 5. Error Handling trong React

#### Mô tả

Error handling là quá trình xử lý các lỗi xảy ra trong quá trình thực thi ứng dụng React, từ lỗi logic đến lỗi mạng. Điều này giúp đảm bảo ứng dụng hoạt động ổn định và cung cấp trải nghiệm người dùng tốt hơn.

#### Ví dụ

```javascript
import React, { useState } from 'react';

const ErrorHandlingComponent = () => {
  const [error, setError] = useState(null);
  const [data, setData] = useState(null);

  const fetchData = async () => {
    try {
      const response = await fetch('https://api.example.com/data');
      const result = await response.json();
      setData(result);
    } catch (error) {
      setError(error.message);
    }
  };

  return (
    <div>
      {error && <p>Error: {error}</p>}
      {data ? (
        <ul>
          {data.map(item => (
            <li key={item.id}>{item.name}</li>
          ))}
        </ul>
      ) : (
        <button onClick={fetchData}>Fetch Data</button>
      )}
    </div>
  );
};

export default ErrorHandlingComponent;
```
### 6. Throttling trong React

#### Mô tả

Throttling là một kỹ thuật quan trọng trong React để giới hạn tần suất gọi hàm trong các tình huống như xử lý sự kiện scroll, resize hay các tương tác người dùng khác. Nó giúp giảm tải xử lý và tối ưu hóa hiệu suất của ứng dụng.

#### Ví dụ

```javascript
import React, { useState, useEffect } from 'react';

const ThrottlingComponent = () => {
  const [scrollPosition, setScrollPosition] = useState(0);

  const throttle = (func, limit) => {
    let throttling = false;
    return function (...args) {
      if (!throttling) {
        func.apply(this, args);
        throttling = true;
        setTimeout(() => {
          throttling = false;
        }, limit);
      }
    };
  };

  const handleScroll = () => {
    setScrollPosition(window.scrollY);
  };

  const throttledScroll = throttle(handleScroll, 200); // Throttle limit: 200ms

  useEffect(() => {
    window.addEventListener('scroll', throttledScroll);
    return () => {
      window.removeEventListener('scroll', throttledScroll);
    };
  }, [throttledScroll]);

  return (
    <div style={{ height: '200vh' }}>
      <p>Scroll Position: {scrollPosition}</p>
    </div>
  );
};

export default ThrottlingComponent;
```
### 7. Lazy Loading và Code Splitting trong React

#### Mô tả

Lazy Loading và Code Splitting là hai kỹ thuật quan trọng trong React để tối ưu hóa tải trang và cải thiện hiệu suất ứng dụng bằng cách tải các phần của ứng dụng chỉ khi chúng cần thiết.

#### Lazy Loading

##### Ví dụ

```javascript
import React, { lazy, Suspense } from 'react';

const LazyComponent = lazy(() => import('./LazyComponent'));

const App = () => (
  <Suspense fallback={<div>Loading...</div>}>
    <LazyComponent />
  </Suspense>
);

export default App;
```
#### Code Splitting

##### Ví dụ
```javascript
import React, { useState } from 'react';

const CodeSplittingComponent = () => {
  const [showComponent, setShowComponent] = useState(false);

  const loadComponent = async () => {
    const module = await import('./DynamicComponent');
    // 'module' contains the exported module content
    setShowComponent(true);
  };

  return (
    <div>
      <button onClick={loadComponent}>Load Dynamic Component</button>
      {showComponent && <DynamicComponent />}
    </div>
  );
};

export default CodeSplittingComponent;
```

### 8. Virtualized Lists trong React

#### Mô tả

Virtualized Lists là một kỹ thuật để hiển thị danh sách lớn của các phần tử một cách hiệu quả trong React bằng cách chỉ render những phần tử nằm trong phạm vi khung nhìn của người dùng.

#### Ví dụ sử dụng react-window

```javascript
import React from 'react';
import { FixedSizeList } from 'react-window';

// Component dùng để render từng hàng của danh sách
const Row = ({ index, style }) => (
  <div style={style}>
    Row {index}
  </div>
);

const VirtualizedListComponent = () => (
  <FixedSizeList height={400} width={300} itemSize={50} itemCount={100}>
    {Row}
  </FixedSizeList>
);

export default VirtualizedListComponent;
