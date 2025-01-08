---
layout: post
section-type: post
has-comments: true
title: CI cho người mới bắt đầu cùng với Github Actions - Phần 1
category: tech
tags: ["tutorial", "programing", "devops", "nodejs"]
---

CI không còn là khái niệm xa lạ trong thế giới phát triển phần mềm. Tuy nhiên, nhiều người vẫn nghĩ rằng CI chỉ dành cho các dự án lớn hoặc các công ty có đội ngũ DevOps chuyên nghiệp. Thực tế, việc xây dựng một pipeline CI đơn giản lại vô cùng dễ dàng, ngay cả với các dự án cá nhân.

Bài viết này sẽ hướng dẫn bạn từng bước để tích hợp CI vào dự án Node.js của mình bằng GitHub Actions, giúp bạn tự động hóa quá trình phát triển phần mềm và đảm bảo chất lượng code.

#### Để bắt đầu, kiểm tra xem bạn đã có những thứ này chưa nhé
- Một tài khoản GitHub
- Một dự án Node.js "có thể chạy"
- Kiến thức cơ bản về Git và Bash
- Optional: một máy chủ riêng nếu muốn deploy lên đó.

#### Bước 1: Tạo một GitHub repo mới
Nếu bạn đã lưu sẵn dự án trên Github, lướt qua thôi. Nếu chưa có thì có thể tạo mới hoặc add vào dự án trên máy mình cũng được.

#### Bước 2: Kiểm tra lại dự án Node.js của bạn
##### a/ Đã có unit test
Unit test gần như là công việc bắt buộc khi viết một dòng code mới, mình biết rằng đôi khi sự "lười biếng" sẽ khiến bạn "cố tình" quên viết UT. Nhưng nếu không có UT, CI của bạn sẽ gần như vô dụng hoặc là sẽ không hiệu quả.

Có nhiều thư viện hỗ trợ UT, trong bài viết mình đang sử dụng `jest`

##### b/ Cấu hình cho các `scripts` trong `package.json`
```json
"scripts": {
    "dev": "nodemon --import=tsx src/app.js",
    "test": "jest",
    "build": "rimraf ./build && tsc",
    "start": "npm run build && node ./build/app.js"
  },
```
- Ví dụ trên mình có sử dụng thêm thư viện `nodemon` để app khi chạy trên local tự động cập nhật nếu có thay đổi.
- Ví mình sử dụng typescript nên khi chạy trên local mình có thêm --import=tsx để đỡ phải build.
- Cài thêm tool `rimraf` để hỗ trợ làm sạch thư mục build của dự án (nó tương tự như câu lệnh rm -rf)
- Để test scripts trên local, có thể sử dụng

```bash
npm run dev

npm run build

npm run start
```
<br>
#### Bước 3: Thiết lập GitHub Actions workflow 
- Nhấn vào tab "Actions" trong repo GitHub của bạn.
- Có thể chọn từ những mẫu có sẵn hoặc một workflow trắng.
- Vì bạn là người mới, hãy bắt đầu bằng chọn workflow có sẵn nhé.

<img src="/img/posts/github_actions.png" alt="Github workflow init">

- GitHub sẽ tạo 1 file mới cho bạn trong thư mục .github/workflows như sau

```yml
name: Node.js CI

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

jobs:
  build:

    runs-on: ubuntu-latest

    strategy:
      matrix:
        node-version: [18.x, 20.x, 22.x]
        # See supported Node.js release schedule at https://nodejs.org/en/about/releases/

    steps:
    - uses: actions/checkout@v4
    - name: Use Node.js ${{ matrix.node-version }}
      uses: actions/setup-node@v4
      with:
        node-version: ${{ matrix.node-version }}
        cache: 'npm'
    - run: npm ci
    - run: npm run build --if-present
    - run: npm test
```

Đừng hoảng, xem từng dòng có ý nghĩa gì nhé:
- `on:` sự kiện để kích hoạt workflow này, đó là khi có thay đổi trên branch `main` -> workflow sẽ chạy hoàn toàn tự động. Để workflow chạy thủ công khi có nhu cầu, có thể thay bằng `on: workflow_dispatch`
- `jobs` các tác vụ sẽ làm 
  + `build`: tên tác vụ, sau này để phân biệt khi làm pipline có nhiều jobs
  + `runs-on` & `strategy` môi trường và các thiết lập
  + `steps` các bước thực hiện: checkout code > cài đặt môi trường của nodejs
  + `run` các câu lệnh thực tế từ dự án. ở đây chúng tả chỉ `clean install`, `build` và `test`

Commit thay đổi và worflow sẽ được chạy lần đầu tiên.

<img src="/img/posts/github_actions_2.png" alt="Github workflow action result">

Bạn có thể nhấn vào tên workflow và xem kết quả của từng bước chạy mình đã cấu hình.
Từ đây, mỗi khi bạn push code lên git, workflow này sẽ tự động chạy. Bạn sẽ biết được code mới của mình có failed UT nào.
<img src="/img/posts/github_actions_3.png" alt="Github workflow action detail">


Đón xem phần 2 mình sẽ viết thêm về workflow để chạy và deploy trên server cá nhân. Mọi người để lại bình luận để ủng hộ mình nhé.