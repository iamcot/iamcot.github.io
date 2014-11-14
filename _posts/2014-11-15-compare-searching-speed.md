---
title: Compare Searching Speed
layout: post
author: CoT
url: /2014-11-15-compare-searching-speed
path: 2014-11-15-compare-searching-speed.md
---
So sánh tốc độ các thuật toán tìm kiếm và so sánh cơ bản

Nhân tiện có ticket trên công ty, cần viết 1 đoạn code nhỏ để tìm kiếm 1 email cho trong 1 chuỗi cách nhau bằng dấu phẩy.

Thuật toán lớp 1 dev nào cũng biết

1. Tách chuỗi thành mảng
2. Lặp mảng đó và lọc khoảng trắng
3. Dùng hàm in_array để tìm kiếm.

Cải tiến một chút, thì trong khi trong khi bỏ khoảng trắng ta kế hợp tìm kiếm và break khi tìm thấy.

Tuy nhiên đây là chỉ với trường hợp mảng tách ra chỉ dùng để tìm kiếm 1 lần, nếu mảng đó được sử dụng nhiều lần để tìm kiếm thì cách trên có cồn tối ưu?

Thử hình dung nếu dùng in_array() hoặc tự lặp lại mảng trên để đối chiếu và xuất ra vị trí thì càng dùng nhiều thì tốc độ càng chậm.

Tuy nhiên nếu tìm kiếm dụa trên key bằng hàm isset() thì thế nào?

Thực nghiệm đã chứng tỏ rằng, dùng isset() sẽ có tốc độ nhanh hơn gấp nhiều lần.

Như vậy thuật toán của chúng ta bây giờ là:
1. Tách chuỗi thành mảng
2. Lặp mảng, lọc khoảng trắng và gán mảng mới[phần tử]='';
3. Mỗi lần muôn biết chuỗi tìm kiếm có trong mảng hay không, chỉ cần gọi hàm isset.

Bonus 1 chút, có người nói so sánh theo kiểu bool sẽ nhanh hơn kiểu khác, nhưng theo thực nghiệm đo đạc thì.. chả thấy khác gì cả -_-
ai có cao kiến về vụ này xin chỉ giáo ạ

