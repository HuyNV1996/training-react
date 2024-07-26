# CÁC THƯ VIỆN HỖ TRỢ VIỆC FETCH DATA VÀ CACHE

Đầu tiên hãy nhìn đoạn code logic fetch data dưới đây

```ts
import React, { useState, useEffect } from "react";

function FetchData() {
    const [data, setData] = useState(null);
    const [loading, setLoading] = useState(true);
    const [error, setError] = useState(null);

    useEffect(() => {
        const fetchData = async () => {
            setLoading(true);
            try {
                const response = await fetch("https://api.example.com/data");
                if (!response.ok) {
                    throw new Error("Network response was not ok");
                }
                const result = await response.json();
                setData(result);
            } catch (error) {
                setError(error);
            }
            setLoading(false);
        };

        fetchData();
    }, []);

    if (loading) {
        return <div>Loading...</div>;
    }

    if (error) {
        return <div>Error: {error.message}</div>;
    }

    return (
        <div>
            <h1>Data fetched from API:</h1>
            <pre>{JSON.stringify(data, null, 2)}</pre>
        </div>
    );
}

export default FetchData;
```

Chỉ với việc xử lý gọi API và quản lý các state, với cách thông thường như trên thực sự là rất dài, và đôi lúc nó là lặp đi lặp lại các đoạn logic này với mọi api, chẳng lẽ với lần gọi api nào chúng ta cũng phải viết 1 đống code như thế?

Vì vậy các thư viện Fetch data được ra đời

Hãy nhìn 1 đoạn code với kết quả tương tự khi áp dụng React Query

```ts
import React from "react";
import { useQuery } from "react-query";

function DataComponent() {
    const { data, error, isLoading } = useQuery(
        "fetchData",
        fetch("https://api.example.com/data")
    );
    if (isLoading) {
        return <div>Loading...</div>;
    }
    if (error) {
        return <div>Error: {error.message}</div>;
    }
    return (
        <div>
            <h1>Data</h1>
            <pre>{JSON.stringify(data, null, 2)}</pre>
        </div>
    );
}
```

### Lý do các thư viện Fetch Data

Giúp chúng ta hạn chế những việc lặp đi lặp lại trong quá trình fetch data.

Để fetch data trong React

-   Khai báo useEffect và gọi API trong đó
-   Xử lý cleanup function để tránh việc gọi duplicate data
-   Tracking trạng thái loading để hiển thị skeleton
-   Quản lý thời gian cache khi user tương tác với UI

Những việc này không khó, nhưng nó nhiều, nếu nhiều component cần implement cái này thì khá mệt.

# RTK QUERY

RTK query là thư viện thuộc hệ sinh thái Redux giúp chúng ta quản lý việc gọi API và caching dễ dàng.

### Các tính năng chính của RTK Query:

1. **Tích hợp với Redux Toolkit**:

    - RTK Query được thiết kế để tích hợp chặt chẽ với Redux Toolkit, cung cấp một phương pháp trực quan và hiệu quả để quản lý trạng thái liên quan đến dữ liệu từ API. Thông qua việc sử dụng createApi, bạn có thể tạo ra các slice API với cấu hình đơn giản, đồng thời tận dụng các tính năng của Redux Toolkit như middleware và reducer.

2. **Tạo endpoints dễ dàng**:

    - RTK Query cho phép định nghĩa các endpoints API một cách dễ dàng thông qua phương thức createApi. Ví dụ, bạn có thể tạo các truy vấn và mutations bằng cách sử dụng builder.query và builder.mutation, cung cấp các cấu hình cho từng điểm cuối API.

```js
import { createApi, fetchBaseQuery } from "@reduxjs/toolkit/query/react";

const api = createApi({
    reducerPath: "api",
    baseQuery: fetchBaseQuery({ baseUrl: "/api" }),
    endpoints: (builder) => ({
        getPosts: builder.query({
            query: () => "posts",
        }),
        addPost: builder.mutation({
            query: (newPost) => ({
                url: "posts",
                method: "POST",
                body: newPost,
            }),
        }),
    }),
});

export const { useGetPostsQuery, useAddPostMutation } = api;
```

3. **Caching tự động**:

    - RTK Query tự động quản lý cache cho các dữ liệu API bằng cách lưu trữ và tái sử dụng dữ liệu từ các yêu cầu trước đó. Điều này giúp giảm thiểu số lượng yêu cầu tới server và cải thiện hiệu suất ứng dụng. Cache có thể được cấu hình để làm mới hoặc xóa theo nhu cầu của ứng dụng.

4. **Refetching và Polling**:

    - RTK Query hỗ trợ tự động refetching khi các sự kiện như lấy lại focus trên tab trình duyệt hoặc khôi phục kết nối mạng xảy ra. Đồng thời, bạn có thể cấu hình polling để tự động làm mới dữ liệu theo khoảng thời gian định kỳ bằng cách sử dụng thuộc tính pollingInterval trong cấu hình endpoint.

5. **Optimistic Updates**:
    - RTK Query giúp cải thiện trải nghiệm người dùng bằng cách cập nhật giao diện người dùng ngay lập tức trước khi nhận được phản hồi từ server.

### Cách sử dụng RTK Query:

### Bước 1: Cài đặt

```bash
npm install @reduxjs/toolkit react-redux
```

### Bước 2: Tạo API Slice với JavaScript

```javascript
import { createApi, fetchBaseQuery } from "@reduxjs/toolkit/query/react";

// Tạo API slice
const api = createApi({
    reducerPath: "api",
    baseQuery: fetchBaseQuery({ baseUrl: "/api" }),
    endpoints: (builder) => ({
        // Fetch data
        getPost: builder.query({
            query: (id) => `get-post/${id}`,
        }),
        // Mutate data
        updatePost: builder.mutation({
            query: (post) => ({
                url: `update-post/${post.id}`,
                method: "PUT",
                body: post,
            }),
        }),
    }),
});

export const { useGetPostQuery, useUpdatePostMutation } = api;
export default api;
```

### Bước 3: Cấu hình store

```javascript
import { configureStore } from "@reduxjs/toolkit";
import api from "./services/api";

const store = configureStore({
    reducer: {
        [api.reducerPath]: api.reducer,
    },
    middleware: (getDefaultMiddleware) =>
        getDefaultMiddleware().concat(api.middleware),
});

export default store;
```

### Bước 4: Tạo và sử dụng Component để hiển thị bài viết và cập nhật bài viết

```javascript
import React, { useState } from "react";
import { useGetPostQuery, useUpdatePostMutation } from "./services/api";

const Post = ({ postId }) => {
    const { data, error, isLoading } = useGetPostQuery(postId);
    const [updatePost, { isLoading: isUpdating, error: updateError }] =
        useUpdatePostMutation();
    const [newTitle, setNewTitle] = useState("");

    if (isLoading) return <div>Loading...</div>;
    if (error) return <div>Error occurred</div>;

    const handleUpdate = () => {
        updatePost({ id: postId, title: newTitle });
    };

    return (
        <div>
            <h1>{data?.title}</h1>
            <p>{data?.body}</p>
            <input
                type="text"
                value={newTitle}
                onChange={(e) => setNewTitle(e.target.value)}
                placeholder="New title"
            />
            <button onClick={handleUpdate} disabled={isUpdating}>
                {isUpdating ? "Updating..." : "Update Title"}
            </button>
            {updateError && <div>Error updating post</div>}
        </div>
    );
};

export default Post;
```

### Bước 5: Tích hợp Component vào ứng dụng

```javascript
import React from "react";
import ReactDOM from "react-dom";
import { Provider } from "react-redux";
import store from "./store";
import Post from "./Post";

const App = () => {
    return (
        <Provider store={store}>
            <div>
                <h1>Post Details</h1>
                <Post postId={1} />
            </div>
        </Provider>
    );
};

ReactDOM.render(<App />, document.getElementById("root"));
```

Với ví dụ này, bạn có thể sử dụng `useGetPostQuery` để lấy dữ liệu bài viết và `useUpdatePostMutation` để cập nhật bài viết. Các hàm hook này được tự động sinh ra từ API slice đã định nghĩa và có thể được sử dụng trong các component React .

## Cơ chế Cache của RTK Query

Caching là một tính năng quan trọng của RTK Query. Khi chúng ta fetch dữ liệu từ server, RTK Query sẽ cache dữ liệu vào Redux. Tất nhiên đây là cache trên RAM => F5 lại là mất

Caching sẽ dựa vào

-   API endpoint ( `getPosts`, `getPost`)
-   Query params được sử dụng (ví dụ `1` là param trong `useGetPostQuery(1)`)
-   Số lượng active subscription cộng dồn

Khi một component được mounted và gọi `useQuery` hook, thì component đó subcribe cái data đó => Ta có 1 subsciption, nếu nó unmount thì ta sẽ trở lại 0 (unsubcribe)

Khi request được gọi, nếu data đã được cache thi thì RTK sẽ không thực hiện request mới đến server mà trả về data cache đó

Số lượng subscription được cộng dồn khi mà cùng gọi 1 endpoint và query param. Miễn là còn component subcribe data thì data nó chưa mất, nếu không còn component nào subcribe thì mặc định sau 60s data sẽ xóa khỏi cache (nếu lúc đó có component nào subcribe lại data đó thì còn dữ tiếp)

## Ví dụ về thời gian cache

```jsx
import { useGetUserQuery } from "./api.ts";

function ComponentOne() {
    const { data } = useGetUserQuery(1);
    return <div>...</div>;
}

function ComponentTwo() {
    const { data } = useGetUserQuery(2);
    return <div>...</div>;
}

function ComponentThree() {
    const { data } = useGetUserQuery(3);
    return <div>...</div>;
}
function ComponentFour() {
    const { data } = useGetUserQuery(3);
    return <div>...</div>;
}
```

Khi 4 component trên được gọi thì ta có

-   Component 1 subcribe data 1
-   Component 2 subcribe data 2
-   Component 3 và 4 cùng subcribe data 3

Chỉ có 3 request được gửi lên server là request từ component 1,2,3. Còn component 4 sẽ dùng lại data cache từ component 3

Data sẽ được giữ lại cho đến khi không còn component nào subcribe. Ví dụ:

-   Nếu component 1 hoặc 2 bị unmount, data 1 hoặc data 2 sẽ bị xóa sau 60s
-   Nếu component 3 bị unmount, data 3 vẫn còn vì component 4 vẫn đang subcribe. Nếu lúc này 4 unsubcribe thì data 3 mới bị xóa sau 60s

# React Query

## React Query là gì?

TanStack Query (tên mới) hay React Query là thư viện giúp quản lý các state bất đồng bộ như data từ api.

Sức mạnh của Tanstack Query

-   Quản lý cache data và cập nhật cực kỳ đơn giản với zero config
-   Không dùng global state, reducer để quản lý, không học thuật khó hiểu.
-   Có khả năng tương thích và mở rộng với mọi use-case

Tanstack Query không đảm nhận việc gọi API, việc gọi API sẽ thực hiện thông qua các thư viện bạn dùng như axios, fetch API. Còn Tanstack Query chỉ đảm nhận việc quản lý data và trigger khi cần thiết.

## Cách sử dụng

### Bước 1: Cài đặt

Trước tiên, bạn cần cài đặt React Query và React Query Devtools:

```bash
npm install react-query
npm install @tanstack/react-query-devtools
```

### Bước 2: Cấu hình `QueryClient` và `QueryClientProvider`

Tạo một tệp cấu hình cho React Query, nơi bạn sẽ thiết lập `QueryClient` và bọc ứng dụng của bạn bằng `QueryClientProvider`.

```javascript
// src/queryClient.js
import { QueryClient } from "@tanstack/react-query";

const queryClient = new QueryClient();

export default queryClient;
```

Bọc ứng dụng của bạn bằng `QueryClientProvider` trong tệp chính:

```javascript
// src/index.js
import React from "react";
import ReactDOM from "react-dom";
import { QueryClientProvider } from "@tanstack/react-query";
import queryClient from "./queryClient";
import App from "./App";
import { ReactQueryDevtools } from "@tanstack/react-query-devtools";

ReactDOM.render(
    <React.StrictMode>
        <QueryClientProvider client={queryClient}>
            <App />
            <ReactQueryDevtools initialIsOpen={false} />
        </QueryClientProvider>
    </React.StrictMode>,
    document.getElementById("root")
);
```

### Bước 3: Tạo và sử dụng các hook để truy vấn dữ liệu

Sử dụng `useQuery` để thực hiện các truy vấn dữ liệu từ API và `useMutation` để thực hiện các thao tác thay đổi dữ liệu (như POST, PUT, DELETE).

#### Truy vấn dữ liệu với `useQuery`

```javascript
// src/components/Posts.js
import React from "react";
import { useQuery } from "@tanstack/react-query";

const fetchPosts = async () => {
    const response = await fetch("/api/posts");
    if (!response.ok) {
        throw new Error("Network response was not ok");
    }
    return response.json();
};

const Posts = () => {
    const { data, error, isLoading } = useQuery(["posts"], fetchPosts);

    if (isLoading) return <div>Loading...</div>;
    if (error) return <div>Error occurred: {error.message}</div>;

    return (
        <ul>
            {data.map((post) => (
                <li key={post.id}>{post.title}</li>
            ))}
        </ul>
    );
};

export default Posts;
```

#### Thực hiện thao tác thay đổi dữ liệu với `useMutation`

```javascript
// src/components/AddPost.js
import React, { useState } from "react";
import { useMutation, useQueryClient } from "@tanstack/react-query";

const addPost = async (newPost) => {
    const response = await fetch("/api/posts", {
        method: "POST",
        headers: {
            "Content-Type": "application/json",
        },
        body: JSON.stringify(newPost),
    });
    if (!response.ok) {
        throw new Error("Network response was not ok");
    }
    return response.json();
};

const AddPost = () => {
    const [title, setTitle] = useState("");
    const [body, setBody] = useState("");
    const queryClient = useQueryClient();

    const mutation = useMutation(addPost, {
        onSuccess: () => {
            // Gọi lại query posts lấy dữ liệu mới sau khi cập nhật thành công
            queryClient.invalidateQueries(["posts"]);
        },
    });

    const handleSubmit = (event) => {
        event.preventDefault();
        mutation.mutate({ title, body });
    };

    return (
        <form onSubmit={handleSubmit}>
            <input
                type="text"
                value={title}
                onChange={(e) => setTitle(e.target.value)}
                placeholder="Title"
            />
            <textarea
                value={body}
                onChange={(e) => setBody(e.target.value)}
                placeholder="Body"
            />
            <button type="submit" disabled={mutation.isLoading}>
                {mutation.isLoading ? "Adding..." : "Add Post"}
            </button>
            {mutation.isError ? (
                <div>Error occurred: {mutation.error.message}</div>
            ) : null}
            {mutation.isSuccess ? <div>Post added!</div> : null}
        </form>
    );
};

export default AddPost;
```

### Tính năng nổi bật của React Query:

1. **Caching và Background Updates**:

    - Dữ liệu được cache và cập nhật nền tự động giúp cải thiện hiệu suất và giảm số lượng yêu cầu không cần thiết.

2. **Automatic Refetching**:

    - Dữ liệu có thể được tự động refetch khi có sự thay đổi về focus hoặc khi kết nối mạng được khôi phục.

3. **Pagination và Infinite Query**:

    - Hỗ trợ phân trang và tải dữ liệu vô hạn, giúp quản lý dữ liệu lớn hiệu quả.

4. **DevTools**:

    - Cung cấp các công cụ gỡ lỗi giúp kiểm tra và phân tích trạng thái các truy vấn và mutations.

5. **Optimistic Updates**:

    - Hỗ trợ cập nhật lạc quan giúp cải thiện trải nghiệm người dùng bằng cách cập nhật giao diện ngay lập tức trước khi nhận được phản hồi từ server.

6. **Query Invalidations và Refetching**:
    - Hỗ trợ invalidation và refetching của các truy vấn để đảm bảo dữ liệu luôn được cập nhật.

React Query là một công cụ mạnh mẽ cho việc quản lý dữ liệu trong các ứng dụng React, giúp đơn giản hóa các thao tác với API và cải thiện hiệu suất và trải nghiệm người dùng.

## Một số khái niệm quan trọng

-   `staleTime` (default `0` ms): Thời gian data được cho là đã cũ. Khi get data xong thì sau một thời gian bạn quy định thì data nó sẽ tự cũ. **Lưu ý cái `stale` trên dev tool nó hiển thị là data của bạn `stale` và `active`**
-   `cacheTime` (default `5*60*1000` ms tức 5 phút): Thời gian data sẽ bị xóa ra khỏi bộ nhớ đệm. Có thể data đã "cũ" nhưng nó chưa bị xóa ra khỏi bộ nhớ đệm vì bạn set `staleTime < cacheTime`. Thường thì người ta sẽ set `staleTime < cacheTime`
-   `inactive`: là khi data đó không còn component nào subcribe cả

```tsx
const result = useQuery({ queryKey: ["todos"], queryFn: fetchTodoList });
```

`result` là một object chứa một vài state rất quan trọng: `status`, `fetchStatus`,...

Những state về các khoảnh khắc của data

-   `isLoading` or `status === 'loading'` - Query chưa có data
-   `isError` or `status === 'error'` - Query xảy ra lỗi
-   `isSuccess` or `status === 'success'` - Query thành công và data đã có sẵn

Những state về data

-   `error` - Nếu `isError === true` thì `error` sẽ xuất hiện ở đây
-   `data` - Nếu `isSuccess === true` thì `data` sẽ xuất hiện ở đây

Đặc biệt là `fetchStatus`

-   `isFetching` or `fetchStatus === 'fetching'` - Đang fetching API.
-   `isPaused` or `fetchStatus === 'paused'` - Query muốn fetch API nhưng bị tạm dừng vì một lý do nào đó.
-   `fetchStatus === 'idle'` - Query không làm gì cả

### Nếu thấy quá rối vì quá nhiều trạng thái, sự khác nhau giữa `status` và `fetchStatus` là như thế nào?

Chỉ cần nhớ

-   `status` cho thông tin `data` có hay không
-   `fetchStatus` cho thông tin về `queryFn` có đang chạy hay không

## Cơ chế caching

Một data mà đã `stale` thì khi gọi lại query của data đó, nó sẽ fetch lại api. Nếu không `stale` thì không fetch lại api (đối với trường hợp `staleTime` giữa các lần giống nhau)

> Còn đối với trường hợp `staleTime` giữa 2 lần khác nhau thì nếu data của lần query thứ 1 xuất hiện lâu hơn thời gian `staleTime` của lần query thứ 2 thì nó sẽ bị gọi lại ở lần thứ 2, dù cho có stale hay chưa.
> Ví dụ: `useQuery({ queryKey: ['todos'], queryFn: fetchTodos, staleTime: 10*1000 })` xuất hiện 5s trước, bây giờ chúng ta gọi lại `useQuery({ queryKey: ['todos'], queryFn: fetchTodos, staleTime: 2*1000 })` thì rõ ràng cái data của lần 1 dù nó chưa được cho là stale nhưng nó xuất hiện 5s trước và lâu hơn thời gian staleTime là 2s nên nó sẽ bị gọi lại ở lần 2.

Một data mà bị xóa khỏi bộ nhớ (tức là quá thời gian `cacheTime`) thì khi gọi lại query của data đó, nó sẽ fetch lại api. Nếu còn chưa bị xóa khỏi bộ nhớ nhưng đã `stale` thì nó sẽ trả về data cached và fetch api ngầm, sau khi fetch xong nó sẽ update lại data cached và trả về data mới cho bạn.

Caching là một vòng đời của:

-   Query Instance có hoặc không cache data
-   Fetch ngầm (background fetching)
-   Các inactive query
-   Xóa cache khỏi bộ nhớ (Garbage Collection)

Một ví dụ:

Giả sử chúng ta dùng `cacheTime` mặc định là **5 phút** và `staleTime` là `0`.

```jsx
function A() {
    const result = useQuery({ queryKey: ["todos"], queryFn: fetchTodos });
}
function B() {
    const result = useQuery({ queryKey: ["todos"], queryFn: fetchTodos });
}
function C() {
    const result = useQuery({ queryKey: ["todos"], queryFn: fetchTodos });
}
```

-   `A` component được mount
    -   Vì không có query nào với `['todos']` trước đó, nó sẽ fetch data
    -   Khi fetch xong, data sẽ được cache dưới key là `['todos']`
    -   hook đánh dấu data là `stale` (cũ) vì sau `0`s
-   Bây giờ thì `B` component được mount ở một nơi nào đó
    -   Vì cache data `['todos']` đã có trước đó, data từ cache sẽ trả về ngay lập tức cho component `B`
    -   Vì cache data `['todos']` được cho là đã `stale` nên nó sẽ fetch api tại component `B`
        -   Không quan trọng function `fetchTodos` ở `A` và `B` có giống nhau hay không, việc fetch api tại `B` sẽ cập nhật tất cả các state query liên quan của `B` và `A` vì 2 component cùng key => cùng subcribe đến một data
    -   Khi fetch thành công, cache data `['todos']` sẽ được cập nhật, cả 2 comonent `A` và `B` cũng được cập nhật data mới
-   Bây giờ thì `A` và `B` unmount, không còn sử dụng nữa, không còn subcribe đến cache data `['todos']` nữa nên data `['todos']` bị cho là `inactive`
    -   Vì `inactive` nên `cacheTime` sẽ bắt đầu đếm ngược 5 phút
-   Trước khi `cacheTime` hết thì ông `C` comopnent được mount. cache data `['todos']` được trả về ngay lập tức cho `C` và `fetchTodos` sẽ chạy ngầm. Khi nó hoàn thành thì sẽ cập nhật lại cache với data mới.
-   Cuối cùng thì `C` unmount
-   Không còn ai subcribe đến cache data `['todos']` trong 5 phút tiếp theo nữa và cache data `['todos']` bị xóa hoàn toàn

# SWR

SWR là React hooks for Data Fetching được phát triển bởi Vercel, với cú pháp cùng cách sử dụng dễ dàng, gọn nhẹ

## Các tính năng

SWR (Stale-While-Revalidate) là một thư viện của React để quản lý trạng thái dữ liệu với các tính năng chính như:

1. **Data Fetching**: SWR tự động quản lý việc lấy dữ liệu từ API hoặc các nguồn dữ liệu khác, giúp giảm thiểu mã code cần viết để xử lý các yêu cầu dữ liệu.

2. **Caching**: Dữ liệu được lưu trữ trong bộ nhớ cache để tăng hiệu suất và giảm số lần gọi API không cần thiết. SWR tự động cập nhật dữ liệu trong bộ nhớ cache khi có sự thay đổi từ server.

3. **Revalidation**: SWR hỗ trợ tính năng revalidation để tự động làm mới dữ liệu khi người dùng truy cập lại trang hoặc khi có các sự kiện nhất định. Điều này giúp đảm bảo dữ liệu luôn được cập nhật và chính xác.

4. **Automatic Fetching**: Dữ liệu được tự động lấy lại (re-fetch) khi cần thiết, chẳng hạn khi trang được tải lại hoặc khi dữ liệu trong cache hết hạn.

5. **Error Handling**: SWR cung cấp các công cụ để xử lý lỗi, giúp bạn dễ dàng xác định và quản lý các lỗi xảy ra trong quá trình lấy dữ liệu.

6. **Pagination & Infinite Loading**: SWR hỗ trợ phân trang và tải dữ liệu vô tận (infinite loading), giúp bạn dễ dàng quản lý các danh sách dữ liệu dài.

7. **Local Mutation**: Bạn có thể thực hiện các thay đổi dữ liệu ngay lập tức trong giao diện người dùng mà không cần phải đợi server trả về kết quả.

8. **Custom Fetchers**: SWR cho phép bạn sử dụng các hàm fetcher tùy chỉnh, giúp bạn linh hoạt trong việc lấy dữ liệu từ các nguồn khác nhau hoặc sử dụng các công cụ khác ngoài `fetch` API.

9. **Conditional Fetching**: Dữ liệu có thể được lấy chỉ khi một điều kiện nhất định được thỏa mãn, giúp giảm thiểu các yêu cầu không cần thiết.

10. **Request deduplication**: SWR sẽ giải quyết vấn đề yếu cầu bị lặp. Do gửi đồng thời nhiều request cùng lúc nên nó sẽ hiểu là chỉ gửi duy nhất một request

SWR rất dễ tích hợp với React và hỗ trợ các tính năng tối ưu hóa hiệu suất mạnh mẽ cho việc quản lý dữ liệu.

## Cách sử dụng

SWR là React Hooks for Data Fetching, được phát triển bởi Vercel

### 1. Cài đặt SWR

```bash
npm install swr
```

### 2. Tạo hàm fetcher và updater

```javascript
// fetcher.js
export const fetcher = (url) => fetch(url).then((res) => res.json());

// updater.js
export const updater = async (url, data) => {
    const response = await fetch(url, {
        method: "PUT",
        headers: {
            "Content-Type": "application/json",
        },
        body: JSON.stringify(data),
    });

    if (!response.ok) {
        throw new Error("Error updating data");
    }

    return response.json();
};
```

### 3. Sử dụng Bound Mutate

```javascript
import useSWR from "swr";
import { fetcher, updater } from "./fetcher";

const Post = ({ postId }) => {
    const { data, mutate, error, isLoading } = useSWR(
        `/api/get-post/${postId}`,
        fetcher
    );

    const handleUpdate = async () => {
        const newTitle = data.title.toUpperCase();
        try {
            // Gửi yêu cầu cập nhật bài viết
            await updater(`/api/update-post/${postId}`, { title: newTitle });

            // Cập nhật dữ liệu cục bộ ngay lập tức và làm mới (refetch)
            mutate({ ...data, title: newTitle }, false); // false để không thực hiện revalidation ngay lập tức
        } catch (err) {
            console.error("Error updating post:", err);
        }
    };

    if (isLoading) return <div>Loading...</div>;
    if (error) return <div>Error occurred</div>;

    return (
        <div>
            <h1>{data?.title}</h1>
            <p>{data?.body}</p>
            <input
                type="text"
                value={data?.title || ""}
                onChange={(e) => handleUpdate(e.target.value)}
                placeholder="New title"
            />
            <button onClick={handleUpdate}>Update Title</button>
        </div>
    );
};

export default Post;
```

### 4. Sử dụng Global Mutate

```javascript
import { useSWRConfig } from "swr";
import useSWR from "swr";
import { fetcher, updater } from "./fetcher";

const Post = ({ postId }) => {
    const { data, error, isLoading } = useSWR(
        `/api/get-post/${postId}`,
        fetcher
    );
    const { mutate } = useSWRConfig();

    const handleUpdate = async () => {
        const newTitle = data.title.toUpperCase();
        try {
            // Gửi yêu cầu cập nhật bài viết
            await updater(`/api/update-post/${postId}`, { title: newTitle });

            // Cập nhật dữ liệu toàn cục
            mutate(
                `/api/get-post/${postId}`,
                { ...data, title: newTitle },
                false
            );
        } catch (err) {
            console.error("Error updating post:", err);
        }
    };

    if (isLoading) return <div>Loading...</div>;
    if (error) return <div>Error occurred</div>;

    return (
        <div>
            <h1>{data?.title}</h1>
            <p>{data?.body}</p>
            <input
                type="text"
                value={data?.title || ""}
                onChange={(e) => handleUpdate(e.target.value)}
                placeholder="New title"
            />
            <button onClick={handleUpdate}>Update Title</button>
        </div>
    );
};

export default Post;
```

### 5. Sử dụng `useSWRMutation`

```javascript
import useSWRMutation from "swr/mutation";

async function updatePost(url, { arg }) {
    const response = await fetch(url, {
        method: "PUT",
        headers: {
            "Content-Type": "application/json",
        },
        body: JSON.stringify(arg),
    });

    if (!response.ok) {
        throw new Error("Error updating post");
    }

    return response.json();
}

const Post = ({ postId }) => {
    const { data, error, isLoading } = useSWR(
        `/api/get-post/${postId}`,
        fetcher
    );
    const { trigger, isMutating } = useSWRMutation(
        `/api/update-post/${postId}`,
        updatePost
    );

    const handleUpdate = async () => {
        const newTitle = data.title.toUpperCase();
        try {
            await trigger({ title: newTitle });
        } catch (err) {
            console.error("Error updating post:", err);
        }
    };

    if (isLoading) return <div>Loading...</div>;
    if (error) return <div>Error occurred</div>;

    return (
        <div>
            <h1>{data?.title}</h1>
            <p>{data?.body}</p>
            <input
                type="text"
                value={data?.title || ""}
                onChange={(e) => handleUpdate(e.target.value)}
                placeholder="New title"
            />
            <button onClick={handleUpdate} disabled={isMutating}>
                Update Title
            </button>
        </div>
    );
};

export default Post;
```

### 6. Tích hợp Component vào ứng dụng

```javascript
import React from "react";
import ReactDOM from "react-dom";
import { SWRConfig } from "swr";
import Post from "./Post";

const App = () => {
    return (
        <SWRConfig value={{ provider: () => new Map() }}>
            <div>
                <h1>Post Details</h1>
                <Post postId={1} />
            </div>
        </SWRConfig>
    );
};

ReactDOM.render(<App />, document.getElementById("root"));
```

### Giải thích:

1. **Bound Mutate**:

    - `mutate` được sử dụng trong hook `useSWR` để cập nhật dữ liệu cục bộ và có thể tùy chọn không thực hiện revalidation ngay lập tức bằng cách truyền `false` cho tham số `revalidate`.

2. **Global Mutate**:

    - `useSWRConfig` cung cấp `mutate` để làm mới dữ liệu cho toàn bộ ứng dụng dựa trên key.

3. **`useSWRMutation`**:
    - Sử dụng hook `useSWRMutation` để thực hiện mutation với khả năng kiểm soát rõ ràng hơn về việc khi nào và cách thực hiện các thay đổi dữ liệu từ xa.

SWR là một thư viện để quản lý dữ liệu trong React, giúp xử lý việc fetch dữ liệu, caching, và tự động cập nhật dữ liệu một cách hiệu quả. Dưới đây là giải thích về cơ chế cache của SWR:

## Cơ chế Cache của SWR

### 1. **Cơ Chế Cache Cơ Bản**

-   **Key-Based Caching**: SWR sử dụng một khóa (key) để lưu trữ dữ liệu trong cache. Khi bạn gọi hook `useSWR(key, fetcher)`, `key` này sẽ được sử dụng để lưu trữ dữ liệu đã fetch vào cache. Nếu có một yêu cầu mới với cùng một `key`, SWR sẽ lấy dữ liệu từ cache thay vì gọi lại API.

### 2. **Cập Nhật và Tái Fetch**

-   **Revalidation**: Khi bạn gọi hook `useSWR`, SWR sẽ kiểm tra cache để xem liệu dữ liệu đã được lưu trữ trước đó hay chưa. Nếu có, nó sẽ trả dữ liệu từ cache ngay lập tức,và nếu data đó được cho là cũ nó tiếp tục gửi một yêu cầu mới để cập nhật dữ liệu (revalidation).

-   **Stale While Revalidate**: Đây là chiến lược caching chính của SWR. Dữ liệu cũ từ cache (stale) sẽ được hiển thị ngay lập tức, trong khi SWR sẽ thực hiện một request mới để lấy dữ liệu cập nhật (revalidate). Điều này giúp đảm bảo rằng người dùng luôn thấy dữ liệu mới nhất mà không phải chờ đợi request API.

### 3. **Chiến Lược Cache**

-   **Deduplication**: SWR tự động gộp nhiều request trùng lặp cho cùng một `key`. Điều này có nghĩa là nếu nhiều component hoặc nhiều hook `useSWR` yêu cầu cùng một dữ liệu, SWR sẽ chỉ gửi một request API duy nhất.

-   **Revalidation On Focus**: Khi bạn quay lại trang hoặc tab, SWR sẽ tự động revalidate dữ liệu để đảm bảo rằng bạn luôn thấy thông tin mới nhất.

-   **Revalidation On Interval**: Bạn có thể cấu hình SWR để thực hiện revalidation theo khoảng thời gian cụ thể, giúp đảm bảo dữ liệu luôn được cập nhật định kỳ.

### 4. **Clear Cache**

-   **Mutate and Revalidate**: Bạn có thể sử dụng hàm `mutate` để cập nhật dữ liệu trong cache hoặc xóa cache để thực hiện một request mới. Ví dụ, nếu bạn biết dữ liệu đã thay đổi, bạn có thể gọi `mutate(key, newData)` để cập nhật cache với dữ liệu mới mà không cần phải đợi một request mới.

# So sánh RTK Query, React Query và SWR

### Về cách triển khai sử dụng

1. **RTK Query**
    - Phụ thuộc vào Redux, nên cách triển khai quen thuộc với những người đã quen Redux
    - Cú pháp dài hơn: RTK Query yêu cầu cấu hình ban đầu và định nghĩa các endpoints, nhưng nó sinh ra các hooks tự động từ cấu hình này.
    - Phức tạp hơn: Cần cấu hình Redux, tạo API slices và hiểu các khái niệm của Redux Toolkit.
2. **React Query**
    - Cấu hình đơn giản hơn, Cần cấu hình QueryClient, nhưng cú pháp trong component đơn giản với các hooks như useQuery và useMutation.
    - Đôi khi có thể phức tạp với các tùy chọn cấu hình nâng cao, nhưng các hook dễ sử dụng cho các truy vấn đơn giản.
    - Dễ dàng sử dụng do cấu hình và cách sử dụng không phức tạp, code dễ hiểu
3. **SWR**
    - SWR có cú pháp đơn giản với hooks và không cần cấu hình phức tạp, chỉ cần cài đặt swr và sử dụng hook.
    - Dễ sử dụng với cú pháp đơn giản, không yêu cầu cấu hình phức tạp
    - Sử dụng key làm endpoint, nên đôi khi không cần định nghĩa các hàm gọi api riêng, chỉ cần định nghĩa hàm chung và gọi nó cho mọi api
    - Có nhiều cú pháp gọn nhẹ giúp xây ứng dụng nhanh chóng

### Về tính năng

-   Mỗi loại đều có thể xử lý tốt gần như trong mọi trường hợp, chỉ khác nhau về cách cấu hình và triển khai
-   **Caching và revalidation**:

    -   RTK Query: Caching endpoint-based, hỗ trợ invalidation và refetching chi tiết.
    -   React Query: Caching mạnh mẽ, refetching tự động, hỗ trợ background updates.
    -   SWR: Caching đơn giản, revalidation tự động và fallback data.

-   **Quản lý trạng thái và lỗi**:

    -   RTK Query: Quản lý trạng thái tải và lỗi chi tiết với các thuộc tính trạng thái.
    -   React Query: Cung cấp trạng thái loading, error và các tính năng mutation hỗ trợ quản lý lỗi và trạng thái.
    -   SWR: Hỗ trợ quản lý lỗi cơ bản, với trạng thái lỗi cơ bản.

-   **Mutation và cập nhật dữ liệu**:

    -   RTK Query: Hỗ trợ mutations, với các tùy chọn refetching và invalidation.
    -   React Query: Hỗ trợ mutations mạnh mẽ, với rollback và optimistic updates.
    -   SWR: Hỗ trợ local mutation với `mutate`, cho phép cập nhật dữ liệu nhanh chóng.

-   **Tính linh hoạt và cấu hình**:
    -   RTK Query: Cấu hình cao, tích hợp với Redux Toolkit.
    -   React Query: Cấu hình linh hoạt với nhiều tùy chọn cho caching và refetching.
    -   SWR: Cấu hình đơn giản, dễ sử dụng nhưng không đầy đủ như các công cụ khác trong một số trường hợp.

## Tóm tắt

### Cách sử dụng:

-   SWR có cách sử dụng đơn giản và gọn nhẹ nhất
-   RTK Query và React Query yêu cầu cấu hình phức tạp hơn.

### Tính năng:

-   React Query và RTK Query cung cấp sẵn nhiều tính năng mạnh mẽ hơn so với SWR.

### Tốc độ:

-   Tất cả ba công cụ đều có hiệu suất cao, nhưng React Query và SWR cung cấp caching và revalidation mạnh mẽ, trong khi RTK Query có thể ảnh hưởng hiệu suất nếu không cấu hình đúng.

## Về độ ưu tiên

-   RTK Query ưu tiên sử dụng trong các hệ thống có tích hợp Redux
-   SWR ưu tiên sử dụng trong các hệ thống NextJS do cùng nhà phát triển là Vercel
-   React Query ưu tiên sử dụng trong đa số các trường hợp còn lại
