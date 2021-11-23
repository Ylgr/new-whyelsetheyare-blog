---
layout: blog
title: "Blockchain thuật sư - Bước 5: Vùng đất mặt trời, vàng và nhịp sống hối hả"
date: 2021-11-23T13:10:57.443Z
top_image: /images/uploads/90137689_p0.jpg
tags:
  - blockchain
  - solana
  - crypto
categories:
  - Lập trình
---
*"Chúng ta không bao giờ có thể đánh giá cuộc đời của người khác, bởi vì mỗi người chỉ biết rõ nỗi đau và sự hy sinh của chính họ. Bạn có thể thấy rằng mình đang đi đúng hướng, nhưng thực ra mỗi người đều có một con đường riêng."*

Rời xa vùng đất Nift yên bình, đến với xứ sở của vàng và ánh mặt trời. Bạn sẽ không khỏi sững sờ trước vẻ đẹp tráng lệ và nhịp sống hối hả tại đây. Đất nước này chạy trên cơ sở nền tảng Solana với tốc độ vượt bậc và phí giao dịch cực rẻ. Điều gì đang xảy ra ở đây, liệu với vẻ ngoài hào nhoáng đó có ẩn chứa một bí mật cực kỳ kinh khủng nào không vì mọi thứ tưởng chừng quá hoàn hảo để có thể tồn tại?

<!-- more -->

# 1. Solana - thế giới không như thế giới ta từng biết

Khi bước vào con đường giả kim này, mọi vận động của thế giới đều phải đánh đổi bằng phí giao dịch. Ở đây cũng không ngoại lệ nhưng vì do đâu phí lại rẻ đến thế?

## 1.1. Program - không phải là smart contract chúng ta từng biết

Khi nhắc đến từ khóa Smart contract, đầu tiên chúng ta đã có cái nhìn qua ngôn ngữ Solidity ở các bước trước. Nhưng tại đây - solana, một thứ như vậy không hề tồn tại mà thay vào đó là Program.

Liệu đây có phải là một tập code quy định logic để cập nhật dữ liệu lên Blockchain đúng không? Đúng vậy.... Thế nó khác quái gì Smart contract???

Và đây là góc nhìn vào cùng một đối tượng đó là token trên nền tảng dưới 2 bài toán: Smart contract và Program.

Smart contract - đại diện là EVM, chúng ta cần một contract cho mỗi token và nó cần phải chứa ít nhất các thông tin: Tên, biểu tượng và số dư của từng địa chỉ ví.

![Cách hình dung của contract](/images/uploads/token.drawio.png "Cách hình dung của contract")

Còn với Program thì sao, để có được token trên Solana, bạn hoàn toàn không cần deploy bất kỳ đoạn code nào trên network cả, tất cả những gì bạn cần là call Program của token để nó sinh ra luôn cho bạn một token và ta-da, bạn đã có nó rồi đó.

![Cách hình dung của Program](/images/uploads/token.drawio-1.png "Cách hình dung của Program")

Và từ đây chính là concepts phân tách ra lối tư duy riêng cho hệ sinh thái này.

## 1.2. Dị cho đến cái ví

Giống như sơ đồ tổng quan trên, để tạo các token, cả fungible token và non-fungible token chúng ta đều dùng một program token duy nhất để call và tạo ra. 

Câu chuyện ko dừng lại ở đó, địa chỉ của bạn vốn ko thể chứa được những loại tài sản nào ngoài solana, nhưng nó có thể own các ví khác nên với mỗi loại tài sản bạn đều cần sinh ra một (hoặc nhiều) ví riêng để đựng nó và được own bởi ví chính của bạn. Khi đó private key của các ví bị own kia sẽ không thể kiểm soát toàn sản trong đó cũng như địa chỉ ví đó sẽ không thể dùng ở một ví khác nữa. Tóm lại là:

![Cách mà solana loại bỏ private key của địa chỉ](https://paulx.dev/assets/img/this_is_pda.8b81f953.jpg "Cách mà solana loại bỏ private key của địa chỉ")

# 2. Solana - Từ siêu rẻ đến ... phải dở túi tiền xem xét

Nếu xem qua các giao dịch trên mạng lưới có tận 4 - 5 chữ số 0 sau dấu phẩy, tính ra việt nam đồng thì mỗi transaction trên Solana sẽ chỉ tốn bằng một tin nhắn SMS thôi nhỉ. Rẻ dữ ta.

Sự thật là đó là ở khía cạnh transaction. Như sơ đồ hình dung về các hoạt động của Solana, chúng ta sẽ cần rất nhiều ví để chứa tiền đúng không? Mỗi ví đó đều cần phí giao dịch từ 0.004 đến 0.01 Solana, thường cỡ 1 đô thời điểm hiện tại đó!

Còn việc deploy program thì sao, nó tốn tận 2-5 Solana cỡ 500 đến 1000 đô la đó!

**Oh my god của Adele!**

Và đó chính là concept chính trong thiết kế của Solana, nếu bạn không phải hình thành các logic mới phù hợp với bussiness của bạn thì bạn không nên sáng tạo.

Bạn cần token? Spl đã có sẵn.

Bạn cần swap? Spl cũng sẵn cung cấp.

Bạn cần NFT? Metaplex sẵn sàng hỗ trợ bạn.

Bạn cần Game play to earn? Bạn đi mà làm!

Bản chất của việc thu fee này là khi bạn sử dụng một account để gắn logic hoặc own các account khác, bạn cần charge phí rent cho 2 năm sử dụng account đó. Xong bạn có thể dùng nó vĩnh viễn và phát sinh ra phí này.

Và điều đáng mừng là nếu bạn ko còn sử dụng account đó nữa thì sao, lỡ tôi bán hết Nift memory dust rồi thì tiền nhà 2 năm tôi vẫn phải đóng à? Tin vui là đến lúc đó thì ta "đóng" luôn account đó luôn để thu hồi tiền rent luôn cũng được.

![Thế này tiện quá](https://img-9gag-fun.9cache.com/photo/a8EKQ31_460s.jpg "Thế này tiện quá")

À còn điều này nữa nha, Program trên Solana viết bằng Rust và um... thật may khi ta có thể dùng mà không cần viết thêm gì cả.

# 3. Những điểm tuyệt vời khác mà Solana mang lại

Bạn nghĩ tôi sẽ ca ngợi tốc độ nhanh kinh khủng với chi phí bỏ ra siêu hời của Solana sao, chắc là vậy đó nhưng tôi không viết đâu bạn qua đây mà đọc: https://coin98.net/solana-sol