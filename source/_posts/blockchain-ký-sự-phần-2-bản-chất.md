---
layout: blog
title: "Blockchain ký sự - Phần 2: Bản chất"
date: 2021-02-15T04:19:20.205Z
toc: true
top_image: https://builtin.com/sites/default/files/styles/medium/public/2019-01/blockchain-companies.jpg
tags:
  - blockchain 
categories:
  - blockchain overview
---
Trong giới kỹ thuật, kiến thức tạo lợi thế và kiến thức phải đến từ cơ sở. Áp dụng lý luận này, hãy áp vào Blockchain và chúng ta sẽ bắt đầu tại đây để hiểu sâu và rõ hơn về cái thứ quỷ này.
<!-- more -->
# 1. Đặc điểm cấu tạo

Blockchain về bản chất là một công nghệ ghép nối từ 3 dạng công nghệ đã có từ trước đó bao gồm: Mật mã học (cryptography), mạng ngang hàng (P2P network) và giao thức lý thuyết trò chơi (game theory protocol).

## 1.1. Cryptography

Cryptography trong một Blockchain network có vai trò khá rộng lớn từ việc làm định danh đến chuẩn giao tiếp cho đến dữ liệu. Nói nôm na đó là cách mà cách các nodes trong mạng nhận dạng nhau, cách lưu dữ liệu vào trong block, cách lưu block vào chain, cách mở / khóa block, ... cho đến cách mà một người sở hữu một loại tài sản nào đó trong mạng lưới.

Bài viết này sẽ chỉ dừng ở cấp độ giới thiệu khái quát, ta sẽ có một chủ đề chuyên sâu về Cryptography sau này.

## 1.2. P2P network

Thông thường, với các hệ thống cơ bản sẽ được bố trí phân phối theo hình thức giao tiếp Client-Server. Với nhiều hệ thống Blockchain, điều này không phải là ngoại lệ nhưng về tổng quan thì không phải. Với phần đa các giao thức Blockchain phổ biến, các node sẽ làm việc với nhau bằng mạng ngang hàng (p2p network). Những Blockchain thế hệ 3.0 hay có sáng tạo bằng việc kết hợp p2p network và client-server thành giao thức hỗn hợp nhưng tổng quan lại thì nhắc đến Blockchain thì sẽ mặc định trước hết là giao thức p2p network.

## 1.3. Game theory protocol

Lý thuyết trò chơi là một trong những chủ đề hot trong giới toán học và kinh tế học, với công nghệ nó cũng là phần không thể thiếu. Trong game theory protocol của Blockchain, những người tham gia đóng vai trò duy trình mạng lưới sẽ bằng cách này hay cách khác nhận được lợi ích từ nó. VD như trong một mạng Proof of Work, các node sẽ đóng vai trò làm miners để xác thực giao dịch và tìm ra đoạn hash khóa block, Node nào tìm ra đoạn hash khóa block sẽ nhận được một lượng coin của mạng lưới làm phần thưởng.

Game theory là một chủ đề rất thú vị, chúng ta sẽ bàn luận nhiều hơn về nó.

# 2. Hình thức hoạt động

Trong giới Blockchain, chúng ta đã có rất nhiều loại Blockchain với những cách hoạt động gần giống nhau. Nên để diễn tả chung về quy trình làm việc, mình sẽ lấy VD về ông tổ của Blockchain: Bitcoin.

![](https://www.weusecoins.com/images/uploads/bitcoin-transaction-life-cycle-high-resolution.png)

Trình tự ở đây sẽ là:

\- Sender tạo transaction request gửi BTC cho Receiver và ký request đó bằng private key để có được raw transaction (là chuỗi ký tự hex dữ liệu).

\- Sender đẩy transaction lên 1 node của mạng Blockchain, node đó sẽ đẩy thông tin transaction lên Bitcoin network.

\- Transaction được xác thực để đảm bảo thông tin gửi đi là xác minh (địa chỉ gửi hợp lệ, địa chỉ nhận hợp lệ, số dư gửi đi hợp lệ, nonce hợp hệ, ...).

\- Khi đã đủ số lượng node verify, transaction sẽ được đẩy vào Block.

\- Block chờ đủ blocktime sẽ được miner tìm ra đoạn hash khóa block (miner nhận được phần thưởng BTC từ việc tính toán ra hash).

\- Block có khóa sẽ gắn vào chain và dữ liệu từ đó sẽ bất biến và tồn tại vĩnh viễn cùng với chain. 

\- Receiver nhận được BTC.

# 3. Cơ chế tự vệ

## 3.1. Tấn công 51%

Mạng p2p với cơ chế hoạt động định nghĩa theo game theory chính là mấu chốt của độ tin cậy thông tin lưu trên chain. Cơ chế bảo toàn thông tin của Blockchain hoạt động theo cơ chế bảo vệ 51%, nghĩa là thông tin lưu trên Blockchain được quy định bởi 51% số node tham gia. 

![](https://vnrebates.net/wp-content/uploads/2020/10/Double-spend-avatar.jpeg)

Với một mạng Blockchain, khi có một đối tượng chiếm trên 51% sức mạnh của mạng lưới, kẻ đó có thể thao túng toàn bộ mạng lưới để sửa đổi thông tin có lợi cho bản thân hắn. Câu chuyện khi đó là những tình huống double spending và được diễn tả nhau sau:

\- Hacker chiếm giữ và sở hữu 51% sức mạnh tính toán.

\- Hacker chuyển tiền cho A bằng transaction X.

\- Transaction X được đưa vào Block Y và gắn vào chain.

\- Hacker sử dụng sức mạnh 51% đảo ngược chain đến Block Y, xóa dữ liệu và tạo lại khóa cho Y, Y+1, ... đến block hiện tại.

\- Dữ liệu X biến mất, Hacker có lại số tiền đã gửi.

Dựa trên câu chuyện trên, khi một Blockchain phải chịu tấn công 51%, giới hạn làm việc của Hacker cũng chỉ dừng lại ở việc thực hiện việc tiêu số tiền mình có nhiều lần và độ khó của việc đó gia tăng nếu block chưa transaction spending đó trôi xa.

Tuy nhiên với một Blockchain, kể cả khi điều đó xảy ra, lớp phòng thủ thứ 2 sẽ dựng lên.

## 3.2. Bất đồng thuận! Fork

Blockchain về bản chất hoạt động dựa theo sự đồng thuận hoạt động giữa các Node với nhau. Khi một nhóm các Node không đồng thuận với hoạt động hiện tại, hiện tượng rẽ nhánh (forking) sẽ diễn ra.

![](https://www.dummies.com/wp-content/uploads/cryptocurrency-hard-fork.jpg)

Quay lại câu chuyện khi một Blockchain bị tấn công 51%. lúc này 49% các Node đang hoạt động thấy có điểm bất thường quyết định thống nhất lại với nhau, dựng lên một mạng Blockchain mới mà không có sự tham gia của 51% Node kia, giữ lại phần lịch sử giao dịch còn đáng tin cậy. Vào thời điểm đó mạng lưới đó sẽ bị tách nhau ra. 

Với người dùng, từ một đồng tiền giờ họ có 2 đồng tiền khác nhau và cạnh tranh nhau về mặt giá trị. Và rồi thị trường cung cầu sẽ phân bổ lại giá trị của 2 đồng tiền này, nếu Hacker tiếp tục lạm dụng sức mạnh của mình ở mạng lưới cũ, đồng tiền của hắn sẽ mất dần giá trị cho đến khi bị kỳ thị.

Hiện tượng Fork cũng diễn ra nhiều trong giới Crypto với nhiều lý do. Tiêu biểu nhất chúng ta có vụ BCH fork ra từ BTC để trở thành bản nâng cấp về sức mạng của BTC.

# 4. Phân loại

Blockchain có nhiều hướng phân loại, mục đích sử dụng, thế hệ, ...

Ở đây chúng ta sử dụng hình thức phân loại phổ thông theo mục đích quản lý và quy mô, Blockchain sẽ phân ra thành 2 loại chính là: Private Blockchain và Public Blockchain.

![](https://www.intheblack.com/-/media/intheblack/allimages/technology/2018/boxes-people-key-illustration.jpg)

## 4.1. Public blockchain

Khi nhắc tới Blockchain thì điều đầu tiên mọi người thường nhắc đến là Public Blockchain, điểm hình là Bitcoin, Ethereum, Binance, ...

Đặc điểm của Public Blockchain là thường có coin đi kèm để làm giá trị mạng lưới khi tham gia. Quyền lợi của những người tham gia mạng lưới là ngang nhau về tổng quan (sức mạnh tính toán trong Proof of Work, số tiền stake trong Proof of Stake, Delegated Proof of Stake, ...).

Với Public Blockchain có một luật, đó là các phẩm code (smart contract, network, ...) cần phải được open source nên mọi người đều có thể đọc, tìm bug và xác minh tính đúng đắn khi tham gia.

Bất kỳ ai có nhu cầu và khả năng đều có thể tham gia Public Blockchain.

## 4.2. Private blockchain

Khác với Public Blockchain, Private Blockchain được xây dựng lên với mục đích kế thừa sức mạnh bảo mật và cách hoạt động theo mô hình phân tán hiệu quả từ Public Blockchain mà thêm vào đó yếu tố phân quyền và xử lý chuyên biệt phục vụ mục đích business.

Gương mặt điển hình trong giới Private Blockchain ta có: Hyperledger và Corda.

So với Public Blockchain, thứ tuyệt vời nhất mà Private Blockchain mang lại là sức mạng và tính linh hoạt, dễ scaling hệ thống.

Private Blockchain thông thường sẽ không cho phép tất cả mọi người tham gia, mỗi đối tượng tham gia đều gắn với định danh và quyền lực theo cấu hình của hệ thống.