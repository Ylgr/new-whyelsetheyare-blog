---
layout: blog
title: "Blockchain thuật sư - Bước 7: Thành lập vương quốc không chính quyền"
date: 2022-04-26T07:23:25.067Z
top_image: /images/uploads/61198831_p0.jpg
tags:
  - blockchain
  - solana
  - crypto
  - spl
categories:
  - Lập trình
---
"Khả năng biến được giấc mơ thành sự thật là cuộc sống trở lên thú vị."

Ở xứ sở Solana này, các quy luật vật lý có phần khác biệt so với phần đa thế giới thuộc layer 3 khác, nơi mà thông tin state không còn là trung tâm của các cuộc nói chuyện. Tại đây, nhờ giao thức fee-payer kết hợp với instructor giúp cho việc bạn có thể lồng nghép các nghiệp vụ centralize lẫn với decentralize một cách dễ dàng và có thể theo cách mà bản thân người tạo và submit transaction không cần chi một đồng phí giao dịch nào để có thể submit. Bài viết này sẽ chỉ chúng ta: How to do that?

<!-- more -->

# 1. Điểm khác biệt

![](https://lorisleiva.com/assets/articles/2021/1122-solana-4-implement-instruction/episode-4-cover.jpg)

Khi Alice chuyển tiền cho Bob thông thường chúng ta gọi đây là một transaction còn ở Solana, nó tính dưới đơn vị instruction.

Bây giờ nha, giải sử Alice chuyển 1 SOL cho Bob, sau đó Bob chuyển lại 1 SOL cho Alice thì sao. Ở các Blockchain phổ biến hiện nay ngoài Solana như Bitcoin, Ethereum hay XRP, ta cần tạo 2 transaction để thực hiện việc này (mặc dù nó chả có ý nghĩa gì), còn ở Solana ta có thể làm được với 1 transaction duy nhất chứa 2 instruction chuyển tiền và chữ ký của cả Alice lẫn Bob, nghe cool chưa!

Chúng ta mở rộng bài toán hơn nha, giờ Alice cần phân phối SOL cho 20 địa chỉ khác, thay vì 20 transaction giờ là 1 transaction duy nhất cần chữ ký của mình Alice, thật tiện. 100 địa chỉ thì sao, thì không dám chắc dùng được trong 1 transaction đâu vì kích thước tối đa của 1 transaction là 1232 bytes (1280 bytes là con số chính xác vì có những đoạn index byte thừa hỗ trợ quá trình serialized).

Điểm thú vị tiếp theo ở Solana là cơ chế feepayer, nói cách khác trong một transaction khi được khởi tạo chúng ta có thể chỉ định tham số này là một địa chỉ cụ thể và điều kiện cần để transaction này được thực thi đó là chữ ký của địa chỉ đó trong transaction.

Hãy tưởng tượng thế này nha, bạn có một tập khách hàng muốn chuyển tiền qua lại. Sau khi lựa chọn hành động và submit action lên server, server sẽ build transaction hộ và chỉ định người chịu phí đó là một ví chịu phí bạn đặt trong hệ thống, sau đó dùng ví đó ký và gửi trả lại cho user. Tại đây user ký thêm lần nữa và đẩy transaction đó lên Blockchain trực tiếp mà không tốn một đồng phí giao dịch nào. Ổn đó chứ. Bạn có thể xem xét một phương pháp khác như sau:

![](https://camo.githubusercontent.com/8ddd87522dfbfd42b05cee1e30e36cc023497d4e72298b67f3ee8d6b5dc71675/68747470733a2f2f63646e2e646973636f72646170702e636f6d2f6174746163686d656e74732f3633383238353039303031383935313137312f3737363431393239353330333137323039362f736f6c67736e2e706e67)

Thử nghĩ xem, cộng đồng Shiba Inu sẽ vui sướng mức nào nếu có thể tự d chuyển SHIB  qua lại mà chỉ dùng SHIB làm phí giao dịch chứ.



# 2. Xây dựng hệ sinh thái nào

