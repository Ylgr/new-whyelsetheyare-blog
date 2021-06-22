---
layout: blog
title: "Blockchain thuật sư - Bước 1: Chuẩn bị hành trang, chúng ta lên đường"
date: 2021-06-22T03:11:35.146Z
top_image: /images/uploads/10_years_of_carciphona_by_shilin_d8v4vyt-fullview.jpg
tags:
  - blockchain
  - lập trình
  - giả kim
categories:
  - Lập trình
---
*"Hãy tự nhủ với trái tim mình rằng nỗi sợ đau khổ còn tồi tệ hơn cả đau khổ. Nhưng không có trái tim nào lại đau khổ khi lên đường tìm kiếm ước mơ của nó"* - Nhà giả kim | Paulo Ceolho

Chào mừng đến với con đường của một giả kim thuật sư nơi chúng ta tìm kiếm cho bản thân mình viên đá tạo vàng. Con đường vốn không dễ dàng gì như tôi đã đề cập trước đó, tuy nhiên cùng nhau chúng ta sẽ đến được nó.

Đầu tiên là hành lý, bạn có thể mang theo bất kỳ thứ gì bạn muốn, ở bước đầu tiên này tôi sẽ giúp bạn chọn ra những món quan trọng nhất.

<!-- more -->

# 1. Bức tranh tổng quan

Ta không thể biết những gì ta không biết. Dưới vai trò cộng sự, trong tầm hiểu biết hạn hẹp của mình, đây là tấm bản đồ dành tặng bạn.

![](/images/uploads/blockchain-map.png)

Với những gì chúng ta thấy thì có vẻ sân đấu này rất rộng nhỉ? Chính xác là vậy đấy, tất cả những việc trên đều ít nhiều đều là đất diễn của chúng ta sau này, đặc biệt là vùng trung tâm bản đồ. Tuyệt vời không?

Uh-hmm! Nghiêm túc lại nào, đây hiện có thể "chưa" là đất diễn bạn có thể bành chướng nên tôi sẽ môt tả qua chút về những điểm đến trong hành trình nha.

Ta sẽ khởi đầu từ dapp nên giờ ta sẽ tiến tới wallet và smart contract đồng thời làm chủ thuộc địa cryptography trong 3 chương tới. Chương thứ 5 tôi sẽ giới thiệu bạn đến với thủ đô của vương quốc Blockchain Core. Tại đây chúng ta sẽ tận dụng những công nghệ tiên tiến để tự ra các vũ trụ Blockchain cho riêng mình, khai phá quyền năng xuyên không (Cross chain) và làm bạn với những người đến từ những vũ trụ khác.

Chúng ta là chúa à, chứ còn gì nữa. Khi bạn đã thạo được Blockchain Core, bạn có thể mở ra các vũ trụ mới, trao sự sống và tri thức cho những sinh vật tại đó.

Còn đá tạo vàng thì sao? Là chúa rồi thì tất nhiên sẽ có quyền năng đó, chỉ cần bạn thành thạo được smart contract, wallet cùng một ít cho state và cryptography. Tiền có thể được bốc ra từ không khí chứ không cần đến chì, mà nó có giá trị hay không thì còn phụ thuộc vào nhiều yếu tố.

# 2. Hành trang cho cuộc hành trình

## 2.1. Hành trang nội tại

Bên trên mô tả có vẻ fantasy nhưng thực tế ngành kỹ thuật không thực sự như thế với bất kỳ ai đâu. Để đạt được  level có thể fantasy hóa việc lập trình thì trước hết đó là tố chất.

Tố chất là năng lực bẩm sinh của mỗi người, là sự hài hòa sinh ra từ tính cách và thể chất để khiến bạn phù hợp với một công việc nào đó. Những người có tốt chất trong bất kỳ lĩnh vực nào cũng đều dễ dàng gặp hái thành công hơn so với những người khác không có.

Làm sao để biến được mình có tốt chất không? Hãy thử qua trắc nghiệm phân loại tính cách MBTI nha, chủ đề này khá thú vị, chúng ta sẽ dành một hai bài viết về nó trong tương lai.

## 2.2. Hành trang kỹ năng

Bạn có tố chất rồi chứ? Tốt, giờ đến kỹ năng lập trình.

Chúng ta ở điểm xuất pháp không phải là chưa có gì. Mặc dù sẽ cùng nhau xuất pháp, trong quá trình học hỏi tôi sẽ giúp bạn khai triển các kỹ năng lập trình phù hợp để giải mã các thử thách trên đường đi. Và những kỹ năng đó chỉ phù hợp với trường hợp đó và một vài trường hợp tương tự.

Trong lộ trình này chúng ta sẽ code qua các ngôn ngữ chính: Solidity, Node.js và Rust.

## 2.3. Hành trang thiết bị

Làm một nhà giả kim thì chắc hẳn phải luôn có trong người đồ nghề rồi, xem nào: rễ cây ngàn tuổi, nọc kiến,... Và chúng ta sẽ không bao giờ dùng đến những thứ đó.

Trong hành trình này tôi sẽ dùng laptop hệ điều hành pop-os 20.04 (tương tự với ubuntu 20.04). Chúng ta khuyến khích code trên ubuntu hoặc mac os thôi, window sẽ rất cực để setup môi trường nhưng nếu bạn thích try hard, chúc bạn may mắn.