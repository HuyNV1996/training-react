### 1. Debouncing và Throttling trong React

#### Mô tả

Debouncing và Throttling là hai kỹ thuật quan trọng để kiểm soát tần suất gọi hàm trong ứng dụng React, đặc biệt là khi xử lý các sự kiện như scroll, resize, hoặc các tương tác người dùng khác.

#### Debouncing

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
### 3.Sử dụng Async/Await trong React

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
