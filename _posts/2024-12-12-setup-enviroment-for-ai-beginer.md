---
layout: post
section-type: post
has-comments: true
title: Bắt đầu với AI sao cho dễ?
category: tech
tags: ["tutorial", "ai"]
---

Bạn muốn nhảy vào thế giới AI mà không biết bơi, nên bắt đầu từ đâu đây?

**Python** thì như một đại dương mênh mông, đầy cá lớn cá bé. Nhưng mà ở Việt Nam, muốn tìm việc làm liên quan đến Python thuần túy trong mảng AI thì hơi khó, giống như đi tìm kim trong đống rơm ấy.

Vậy nên, CoT nghĩ **Node.js** sẽ là một chiếc thuyền nhỏ xinh, vừa đủ để mình khám phá biển cả AI. Thứ nhất, thư viện của nó cũng khá đầy đủ để mình làm những dự án nhỏ và vừa. Thứ hai, Node.js lại rất được lòng các công ty ở Việt Nam, nên cơ hội việc làm cũng sẽ rộng mở hơn.

Node.js không chỉ nhanh như một chiếc xe đua mà còn linh hoạt như một con mèo. Bạn có thể dễ dàng kết hợp Node.js với các thư viện AI phổ biến như TensorFlow.js để xây dựng những ứng dụng thông minh, đáp ứng mọi nhu cầu của người dùng.

Bắt đầu thôi!

!!! Xin lỗi trước là CoT chỉ dùng MacOS nên các ví dụ minh họa cho cài đặt cũng như cú pháp sẽ thuần trên terminal của macOS, mọi người chịu khó tìm hướng dẫn trên OS khác nhé (cũng na ná nhau à)

<br>
### IDE & Extensions

Một IDE thông dụng và khó kiếm được điểm để chê là <a href="https://code.visualstudio.com/" target="_blank" >Visual Studio Code</a> với Dracula theme 

Các extensions đề nghị
- node-snippets

<br>
### NodeJs

Cài từ trang chủ <a href="" target="_blank">Node.Js</a>

Hoặc qua BREW

```bash
# Phiên bản mới nhất (Dec 2024) đang là 22 
# nhưng có vẻ nhiều thư viện bị deprecated quá nên dùng tạm 20 là đủ
brew install node@20

node -v # "v20.18.1" y.z version có nên mới hơn không sao

npm -v # should print "10.8.2" hoặc mới hơn không sao
```
<br>
Node.Js phát triển từ **JS** nên nếu bạn chưa có hoặc chưa vững về js, cũng nên ngó qua <a href="https://www.w3schools.com/js/" target="_blank">JS cơ bản</a>. Các khái niệm sâu hơn mình sẽ lên ở các bài viết sau.

<br>
### APIKEY của OPENAI
Đăng ký tài khoản OPENAI và kích hoạt API Keys miễn phí từ <a href="https://platform.openai.com/api-keys" target="_blank">OPENAI Platform</a>

Key sẽ có dạng 
```
sj-...
```
Với tài khoản free bạn dư sức trải nghiệm với thế giới OpenAI rồi nên đừng lo nhé.

<br>
###  Hello AI World!
Khởi tạo một dự án Node.Js trống
```bash
mkdir hello_ai && cd hello_ai # Tạo thư mục dự án

npm init # Khởi tạo Node
# Bạn sẽ phải khai báo một số thông tin như tên dự án, phiên bản, còn lại tạm thời cứ để mặc định.

touch .env # Tạo một file biến môi trường cho dự án

touch hello.js # Tạo file mã nguồn

npm i openai # Cài đặt module openai client
```

Thêm dòng cấu hình cho **package.json**

```json
  "type": "module",
```
Khai báo OPENAI API Key vào môi trường

```
#! .env
OPENAI_KEY="sk-..."
```

Viết những dòng code đầu tiên để "xin chào" thế giới ai nào!
```js
#! hello.js
import OpenAI from "openai";

const openai = new OpenAI({
    apiKey: process.env.OPENAI_KEY
});

const completion = await openai.chat.completions.create(
    {
        model: "gpt-4o-mini",
        messages:[
            {
                "role": "user",
                "content": "Xin chào open AI"
            }
        ]
    }
);
console.log(completion.choices[0]?.message?.content || "");
```
Khởi chạy đoạn code vừa viết nào 

!!! Mẹo: bạn có thể sử dụng terminal tích hợp trên VSC bằng cách nhấn **Ctrl + `** nhé.

```bash
node --env-file=.env hello.js
```
<br>
Chào mừng! chào mừng đến với AI World.


Bình luận cho mình biết bạn nhận được phản hồi gì từ AI nhé.