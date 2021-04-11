---
layout: blog
title: "Blockchain ký sự - Phần 3: Chữ ký số và các giao dịch"
date: 2021-03-01T05:40:49.328Z
toc: true
top_image: /images/uploads/finance-money-transaction-technology_31965-1134.jpg
tags:
  - blockchain
  - crytocurrency
---
What is it? Then How it work? Tiếp nối seri ký sự này sẽ giải thích cách thức hoạt động của Blockchain từ góc độ nhìn thấy được và đi sâu vào tìm hiểu nó làm cái gì mà ở thời điểm hiện tại lại được tín ngưỡng như vậy.
<!-- more -->
# 1. Transaction là gì?

Transaction (giao dịch) là danh từ đề cập đến sự kiện điều kiện để biến đổi số dư của một tài khoản. Trong Blockchain cũng không ngoại lệ, nó là bản ghi chép dữ liệu chuyển tiền, nhận tiền hay việc kích hoạt làm thay đổi trạng thái của smart contract nào đó (việc này thông thường sẽ tốn phí gas với các mạng như ethereum hay bandwidth với các mạng như EOS).

Transaction trên Blockchain được chia làm 3 loại khác nhau để giải quyết bài toán tránh trùng lặp giao dịch: UTXO, nonce và các loại khác.

# 2. Giải thích hoạt động của transaction

## 2.1. Unspent transaction output (UTXO)

![](https://blog.lopp.net/content/images/uploads/downloaded_images/The-Challenges-of-Optimizing-Unspent-Output-Selection/1-5uICL2T5PLZ4arzHXlA6sQ.png)

Coin điển hình BTC, LTC, BCH, QTUM.

Là kiểu định nghĩa giao dịch đầu tiên của transaction. Một UTXO bao gồm các thông số: input, output, timestamp, hash,....

Khi mỗi giao dịch được thực hiện, sẽ cần require một hoạch nhiều UTXO làm input và sẽ có không hoặc nhiều UTXO khác làm ouput. Ví dụ, khi bạn thực hiện một giao dịch 0.1 BTC, tại thời điểm đó hệ thống đã thống kê bạn có 3 UTXO khác còn lại là 0.06 BTC, 0.03 BTC và 0.05 BTC. Tại thời điểm này giả sử thuật toán ví đã xử lý và chọn 0.06 BTC và 0.03 BTC làm UTXO input, khi đó output sẽ là 0.1 BTC được chuyển đi là 0.02 BTC nhận lại.

Đơn vị sử dụng cho phí giao dịch của những coin này là satoshis/byte. Đồng nghĩa với việc transaction càng ít input và output sẽ càng tiếp kiến chi phí.

Thực tế này đòi hỏi các nhà làm ví cần tìm ra thuật toán tối ưu chọn UTXO cho ví của mình để tối thiểu hóa số tiền phí của user. Vì nhiều trường hơp, cùng gửi 1 số tiền mà user phải chịu 2 khoản phí khác nhau trong khi trả cùng lượng byte fee.

Bằng cách sử dụng UTXO, user có thể revert lại transaction vừa thực hiện (mà chưa được verify) bằng cách sử dụng đúng input của transaction trước và thay thế output đầu ra (yêu cầu tăng byte fee trả cho mạng lưới). Khi đó transaction có fee lớn hơn sẽ được thực hiện trước làm transaction trước đó vi phạm rule và phải revert.

## 2.2. Nonce

![](https://i0.wp.com/cryptodose.co/wp-content/uploads/2020/08/HNN-final-01-01-1.jpg)

Thay vì lưu số dư vào các UTXO, những loại crypto phổ biến khác như ETH, EOS, TROX, ... đã chọn cách xử lý số dư của user trực tiếp trên tài khoản. Khi đó họ cần xử dụng một con số "nonce" để đánh dấu và định danh transaction. Mỗi transaction sẽ có một "nonce" khác nhau và nonce sau yêu cầu cao hơn nonce trước. Bằng cách này transaction sẽ không phải chịu khoản byte fee như kiến trúc UTXO.

Khi sử dụng nonce, ta hoàn toàn có thể revert transaction (pending) bằng cách thực hiện một transaction tương tự cùng số nonce với transaction cũ nhưng thêm fee bỏ ra cho transacction, cách hoạt động tương tự với UTXO.

## 2.3. Khác

Vì khác nên cũng đa dạng lắm loại không như 2 loại trên. Điển hình như những token được xử lý trên mạng Omni.

Omni về bản chất không phải là một blockchain tự vận hành. Sự vận hành của Blockchain này về bản chất là ánh xạ từ Bitcoin sang. Omni bất giờ chỉ đóng vai trò sở hữu những đồng coin trên mạng lưới đó. Lấy ví dụ khi user muốn thực hiện gửi USDT của mình đi, họ phải thực hiện một transaction mà trong đó output của UTXO sẽ là khoản dust 512 satoshis BTC, địa chỉ nhận BTC và mã coin id của USDT là 31 vào output của UTXO.

Nói cách khác Omni sẽ không trực tiếp xử lý giao dịch mà nhờ BTC xác nhận giao dịch và ghi chép lại biến đổi vào số dư người dùng.

# 3. Chữ ký số (digital signature)

![](https://www.smartdatacollective.com/wp-content/uploads/2019/05/digital-signature-data.jpg)

Hãy bắt đầu từ thành phần của transaction. Một transaction sẽ có các thông tin: người gửi, người nhận, số tiền, ... Hay nói tóm lại, transaction là một đối tượng (object). Vậy làm sao để chứng minh được transaction được gửi bởi chính chủ câu trả lời đó chính là chữ ký số.

Khi nói đến chữ ký số, chúng ta có thể hiểu cách hoạt động của thứ này đại loại như cách mà Json Web Token (JWT) hoạt động.

Một object transaction để đẩy lên network yêu cầu trước hết là phải bị biến đổi thành signed transaction bằng private key. Việc sign này sẽ được thực hiện ***hoàn toàn trên ví***. Nói cách khác, nếu bạn dùng một ví client: android, desktop hay cold wallet thì hãy đảm bảo là việc ký thông tin giao dịch có thể hoạt động mà không cần đến internet. Từ đó đảm bảo nguy cơ lộ private key.

Khi đã có signed transaction thì transaction đó được phép đẩy lên blockchain để xác thực và ghi nhận.

Signed transaction cũng như jwt token, bạn không cần private key cũng có thể decode dữ liệu trong đó để đọc được và thêm vào đó, network cũng nhận diện được chữ ký này chính xác do private key của public key đề cập trong transaction thực hiện.