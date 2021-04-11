---
layout: blog
title: "Blockchain ký sự - Phần 1: Blockchain theo năm tháng"
date: 2021-02-03T09:59:20.586Z
toc: true
description: Hiểu đúng trước khi hành động
top_image: /images/uploads/ebefzbywwaadrkh.jpg
tags:
  - blockchain
  - tổng quan
categories:
  - blockchain overview
---
Nếu bạn có trong tay 20 nghìn đồng, vào năm 2007 bạn có thể ăn 2 bát phở. Đến năm 2012 thì chỉ còn được 1 bát và năm 2017 thì một bát phở có giá 30 nghìn. Chuyện gì đang diễn ra ở đây vậy? Đó là khủng hoảng kinh tế! Và với sứ mệnh bảo về đồng tiền của bạn, thể hiện đầu tiên của Blockchain: Bitcoin ra đời.
<!-- more -->
# 1. Mối quan hệ giữa tiền tệ và nền kinh tế

## 1.1. Nơi câu chuyện bắt đầu

  Năm 2007-2008, bong bóng bất động sản vỡ nợ, nhà đất mất giá trầm trọng. Tại thời điểm đó số tiền bỏ ra để mua nhà nhiều nơi còn rẻ hơn số tiền bỏ ra để thuê chúng. Trong bối cảnh đó, hàng loạt ngân hàng cùng hàng vạn người trong tình trạng lung lay vì trước đó là cơn sốt bất động sản, giá nhà đất cao chót vót nên đã trở lên tham lam ôm một đống để rồi bây giờ nhìn vào thì khoản tài sản đó giờ trở lên thật rẻ mạc. Và rồi hàng loạt ngân hàng, doanh nghiệp tuyên bố phá sản dẫn đến người lao động mất việc làm, tiền bạc trở lên khan hiếm và quý báu.

![Bong bóng nhà đất](/images/uploads/ewscripps.brightspotcdn.com.jpg "Bong bóng nhà đất")

  Trước tình cảnh thảm khốc, nhà nước liên tục tuyên bố các chính sách "nới lỏng định lượng" (thẳng thừng nói ra là in tiền ồ ạt) để tung ra hàng loạt các gói cứu trợ nhiều nghìn tỷ đô la đổ vào nền kinh tế. Và rồi nhờ động thái đó, nền kinh tế hồi phục và mọi người thấy mình nhiều tiền hơn trước, hàng hóa cũng theo đó lên giá theo.

## 1.2. Giải thích tình tiết

  Khi chính sách in tiền ồ ạt được thực hiện thì đồng nghĩa với một lượng tiền lớn được đổ vào thị trường, chúng đổ từ đâu nhỉ? Những ngân hàng sắp phá sản à? Đúng! Mà nếu bơm cho đứa đói mà không bơm cho đứa đang sống tốt thì sợ đứa sống tốt thấy thiên vị ỷ đi lười biếng nên phải bơm đều. Thế người lao động được gì từ khoản trợ cấp đó? Họ không được thêm gì cả, chỉ được đảm bảo là công việc của họ ko bị tước mất do doanh nghiệp của họ không bị phá sản thôi.

  Và rồi câu chuyện về sự cung cầu diễn ra, nhiều tiền thì cầu tăng nhưng cung thì vẫn thế dẫn đến tình trạng giá cả các mặt hàng sẽ leo thang để đảm bảo cán cân cung cầu. Khi mà các mặt hàng đều đồng loạt tăng giá, nhu cầu của người lao động vẫn phải được đáp ứng dẫn đến họ phải còng lưng ra làm việc thêm để kiếm lại nguồn cung đủ chu cấp chu nhu cầu cuộc sống trước. Giờ thì số tiền in để cứu kinh tế cuối cùng cũng đến tay người lao động, nhưng rồi kết quả là người lao động giờ phải làm nhiều hơn, kiếm được nhiều tiền hơn ... nhưng vẫn chỉ đủ để phục vụ nhu cầu trước đó.

  Điều gì đang xảy ra nhỉ? Liệu cái từ "vật giá leo thang" có đúng không ta? Không hề, từ chính xác để diễn tả sự kiện này là đồng tiền mất giá!

## 1.3. Câu chuyện tiền tệ

  Trước năm 1971 là thời kỳ tiền bản vị vàng. Khi ấy ứng với mỗi đô la sẽ có thể mang ra ngân hàng chính phủ để đổi lại một lượng vàng nhất định. Lúc đó theo thời gian, thu nhập của người lao động tăng lên và mức sống của họ cũng tăng lên là thật vì lượng vàng khai thác được và trữ trong ngân hàng chính phủ ngày 1 nhiều hơn.

![Fiat](/images/uploads/paper-money-promises.jpg "Fiat")

  Đến năm 1971, dưới thời đại của tổng thống Richard Nixon. Ngài công bố ban hàng lại hình thức tiền tệ mới, thay thế toàn bộ hệ thống tiền bản vị vàng thành tiền pháp định nghĩa là giá trị của đồng tiền giờ đây được đảm bảo bởi uy tín của chính phủ thay vì lượng vàng trong ngân hàng quốc gia. Cũng nhờ chính sách đó, lượng tiền lưu thông cứ từ đó bứt phá tăng lên ồ ạt, tiền mất giá nhanh chóng và cuộc sống của người lao động ngày 1 khó khăn hơn (trên thực tế là vẫn sẽ tốt hơn do khoa học và công nghệ phát triển).

# 2. Blockchain vào cuộc

## 2.1. Thế hệ đầu tiên: Khai sinh và lưu trữ

  Vào những năm 2008, một nhân vật ẩn danh tự xưng là Satoshi Nakamoto đã viết ra bản cáo hạch khai sinh ra một loại tiền điện tử mang tên là Bitcoin và cũng là crypto đầu tiên tồn tại. Bằng sự kết hợp giữa 3 công nghệ: mật mã học, mạng ngang hàng và lý thuyết trò chơi. Một công nghệ mới mang tên Blockchain ra đời.

![Satoshi Nakamoto](/images/uploads/satoshi-nakamoto-01.png "Satoshi Nakamoto")

  Ý tưởng ra đời của Bitcoin là một thứ tiền tệ mà nhà nước không thể kiểm soát được, số tiền sẽ được đào dần theo thời gian nhưng ngày một khó đào hơn cho đến khi không thể đào thêm được nữa. Sự lưu động của dòng tiền được ghi chép lại trên tất cả các sổ cái trên các node p2p cùng. Công nghệ mật mã học giúp mỗi người dùng được định nghĩa một cặp key không trùng nhau để sử dụng. Lý thuyết trò chơi là nền tảng quy chuẩn hóa hoạt động trên toàn mạng lưới với thuật toán đồng thuận Bằng chứng công việc (Proof of work).

  Và chúng ta có Bitcoin của ngày nay.

## 2.2. Thế hệ thứ hai: Hợp đồng thông minh

  Vào những năm 2012, một lập trình viên trẻ tuổi tên Vitalik Buterin đã đề xuất một ý tưởng, đó là sử dụng mạng lưới giao dịch của Bitcoin để lưu trữ dữ liệu phục vụ business. Tuy nhiên ý tưởng này không được cộng đồng Bitcoin đồng thuận. Đến năm 2015, Vitalik quay lại với cương vị là Co-founder của một nền tảng Crypto mới có tên là Etherum cho phép đưa logic và dữ liệu lên mạng lưới Blockchain. Smart contract ra đời từ đây.

  Và chúng ta có Ethereum của ngày nay.

## 2.3. Thế hệ thứ ba: Cải tiến khả năng mở rộng

  Sau quãng thời gian hoạt động, các Blockchain thuộc thế hệ thứ 2 gặp vấn đề về tính mở rộng. Khi mà giá coin ngày càng tăng, khả năng chi trả cho những giao dịch sau này càng khó khăn trong, thuật toán Proof of Work quá tiêu tốn điện năng và đồng thời không thể giới hạn được lượng coin sẽ sinh ra do nhu cầu. 

  Trước tình hình đó thế hệ thứ 3 được khai sinh ra để tập trung giải quyết vấn đề tính mở rộng của Blockchain. Những đặc điểm nổi bật của thế hệ này bao gồm:

\- Layer thứ 2: tạo nền tảng để rút gọn chi phí, giảm thời gian giao dịch (lightning network).

\- Cải thiện thuật toán đồng thuận để giảm sự tiêu hao năng lượng mà vẫn giữ được sự an toàn trong mạng lưới với các thuật toán: Proof of Stake, Delegrated Proof of Stake, Byzantine Fault Tolerance, ...)

\- Directed Acyclic Graphs (đồ thị có hướng không chu trình - GAPs): Giải quyết bài toán chi phí giao dịch và sức mạnh tính toán bằng việc tự sử dụng nguồn tài nguyên có sẵn của người dùng (hoặc của người được chỉ định trong mạng lưới) để đạt thời gian giao dịch nhanh chóng với chi phí gần như bằng không (NANO, IOTA).

# 3. Câu chuyện còn dang dở

  Blockchain là một công nghệ phát triển theo cấp số nhân và tại thời điểm hiện tại, nó đang ở ngay điểm bùng phát. Nghĩa là ở một tương lai gần chúng ta rồi sẽ không còn xa lạ gì với những hệ thống nhận diện hay truy xuất nguồn gốc chạy trên nền tảng Blockchain.

  Phần tiếp theo của seri này sẽ đi vào chủ đề định nghĩa, hoạt động và những kiến thức khác của Blockchain.