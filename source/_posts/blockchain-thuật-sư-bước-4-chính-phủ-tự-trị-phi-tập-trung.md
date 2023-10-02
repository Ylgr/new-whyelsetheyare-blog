---
layout: blog
title: "Blockchain thuật sư - Bước 4: Chính phủ tự trị phi tập trung"
date: 2023-10-02T07:04:23.077Z
top_image: /images/uploads/105230873_p0.jpg
tags:
  - evm
  - dao
categories:
  - Lập trình
---
Bài toán ra quyết định và thực thi, luôn là một bài toán thường trực phải giải quyết cho từng cá nhân hay tập thể. Trong quy mô tập thể khi lợi ích từng bên bị ảnh hưởng ít nhiều trong việc ra quyết định, một chính phủ được hình thành để tiếp nhận tiếng nói chung để ra quyết định và thực thi quyết định đó. Ở thế giới Blockchain, chính phủ này được phổ quát rộng rãi hơn và hiệu quả hơi với tên gọi **Decentralized Autonomous Organization (DAO)**.

Về kỹ thuật, bản chất nó là một smart contract tên Governor.

# Giải thích về Contract Governor

Contract Governor, tùy theo nghiệp vụ sẽ xử lý các chức năng khác nhau nhưng về bản chất, một contract Governor buộc phải có:

- Một hệ thống quy ước tính toán thời gian chuẩn (theo timestamp hay blocknumber hay một đơn vị tùy chỉnh là epoch).
- Một biến dữ liệu lưu lại thông tin các proposal cũng như cập nhật trạng thái của chúng.
- Hệ thống Voting thống kê sức mạnh voting của từng người tham gia hay lựa chọn của họ vào một thời điểm cụ thể.
- Khả năng thực thi hay hủy bỏ một proposal khi cần thiết.

## Clock

Là hệ thống quy chuẩn thời gian dùng trong Governor. Đơn vị phổ biến nhất là block number vì bản chất Blockchain chỉ thực thi khi Block được confirm. Ngoài ra tùy theo nghiệp vụ và bảo mật có thể sử dụng các đơn vị khác để tính toán như timestamp hay epoch quy chuẩn hay từ hoạt động của một smart contract khác.

Nhìn chung Clock phải đảm bảo:
- Được biểu hiện là một con số cụ thể.
- Giá trị tăng dần theo thời gian.

Clock sẽ ảnh hưởng đến toàn bộ logic của những phần khác trong Governor như thời gian tính voting power cho user, thời gian các giai đoạn của một proposal và lịch sử của toàn bộ hoạt động Governor để sử dụng cho một logic cụ thể.

## Propose

Là thể hiện của: Làm gì?

Một propose cơ bản sẽ bao gồm các thông tin:
- Proposer
- Vote start
- Vote end
- Is Executed
- Is Cancel

Ủa? Sao propose lại không lưu thông tin chi tiết của propose làm gì?

Về mặt kỹ thuật, Blockchain chỉ cần lưu Propose hash để làm đối chứng, những thông tin chi tiết được đẩy lên event để sau application tiện query lại. Khi propose qua các giai đoạn và có thể được thực thi thì người thực thi cần đẩy lại chi tiết đầy đủ thông tin đó lên, nếu tạo ra đoạn hash trùng với propose đã lưu thì propose đó hoàn toàn có thể thực thi. Propose hash sẽ là key của những thông tin đã kể trên.

Thế nghĩa là có khả năng exploit execute bằng cách hashing ra đoạn data tương tự nhưng với một mục đích khác?

Điều này cực khó, nếu phải lo lắng về việc này thì phải lo lắng việc private key của Binance cold wallet bị tìm ra trước đã. Vì bản chất việc tìm ra đoạn hash tương tự khác chức năng độ khó tương đương như vậy, mà còn bị ràng buộc trong bối cảnh toàn bộ những thứ Governor có thể làm được còn nhỏ hơn nữa. Thay vì tìm một nguyên tử xác định trong vũ trụ thì đây thậm chí nguyên tử đó khả năng cao chẳng tồn tại nữa.

## Vote

Là thể hiện của quyết định.

Là lựa chọn của những người tham gia hệ thống. Vote có thể quy ước bằng bất cứ giá trị nào tùy theo logic yêu cầu. Hình thức cơ bản nhất của Vote gồm có:
- Against
- For
- Abstain

Chống, thuận và phiếu trắng. Tại sao lại cần phiếu trắng? Hiểu đơn giản thì để logic khi cần một thông số là Quorum - số vote tối thiểu cần để proposal có giá trị. Nó giống như liên hợp quốc khi một quyết định đưa ra như hỗ trợ vũ khí cho Ukraine, nhiều nước phương tây chọn phiếu thuận trong khi Nga, Trung Quốc và đồng minh vote phiếu chống. Phần đa quốc gia trung lập nhưng buộc phải tham gia sẽ vote phiếu trắng.

Ngoài ra Vote còn lưu lại một danh sách địa chỉ đã vote để tiện cho các logic sau.

Thế khi nào proposal được cho là thông qua?

Tùy logic, logic cơ bản nhất là thuận > chống và quorum đảm bảo.

## Execute / Cancel

Dù là quyết định trên giấy tờ, dạng một đề xuất hay quyết định có thể được thực thi onchain thì đều cần được thi hành.

Như trình bày ở trên execute phải được truyền đầy đủ tham số của proposal để có thể thông qua.

Execute cũng khá thoáng, ai thực thi cũng được hết vì bản chất việc thực thi này đến từ chủ thể của Governor.

Thế nếu proposal đó bằng một sai lầm được đẩy lên thì sao? Tính năng Cancel lên tiếng.

Một proposal thông thường có 8 trạng thái:
- Pending: Proposal mới được đẩy lên, chưa thể vote. Mọi người trang thủ chuẩn bị voting power đi.
- Active: Voting power lock, giờ mn vote đi.
- Canceled: Đơn giản là bị hủy bỏ.
- Defeated: Bên đề xuất thua rồi.
- Succeeded: Bên đề xuất thắng nha.
- Queued: Cũng là thắng nhưng tạm thời chưa thực thi được luôn.
- Expired: Hết cả thời gian vote mà chưa xong, hủy.
- Executed: Đã thực thi xong.

# Governor Extensions

Trước khi đi vào Extensions thì có điều này phải làm rõ trước. So với chuẩn ERC20 thì chỉ cần is ERC20 là work smothly không cần quan tâm đến contract làm gì nhưng Governor là khía cạnh khác khi bản thân Governor và toàn bộ extensions đều là abstract, có nghĩa là không thể không tay không bắt giặc buộc phải biết mình cần gì và có thể làm được gì để có thể sử dụng.

Khi xài Extensions giống như thay vì phải quy ước quá nhiều logic thì chỉ cần quy ước bớt logic đi là xài được.

## Governor Counting Simple

Chuẩn và dễ phổ cập nhất trong toàn bộ extensions. Extensions này giúp phần việc quy định giá trị vote thành 3 kiểu như đã đề cập:
- Against
- For
- Abstain

Tính lượng vote dựa theo đó và cho điều kiện để thông qua proposal là for > against.

## Governor Setting

Bản thân Governor là một đề tài để vote, tại sao lại không nhỉ? Smart contract là cho phép vote các thông số setting của governor như:
- Voting delay: Thời gian chờ đến khi bắt đầu vote.
- Voting period: Thời gian từ lúc bắt đầu đến lúc kết thúc vote.
- Proposal threshold: Sức mạnh tối thiểu cần để tạo proposal 

## Governor Timelock Control

Thay vì bản thân Governor là người thực thi của smart contract thì giờ có một smart contract tên là Timelock controller thực thi hộ để deplay viêc thực thi đó lại, cho vào queue. Giải thích cho viêc tại sao proposal lại có state là queue.

## Governor Prevent Late Quorum

Giả sử một con cá voi chờ đến cuối rồi mới nhảy vô thay đổi cục diện kết quả vote thì cũng chẳng lấy gì làm hay ho đúng không? Extensions này cho phép thời gian vote được kéo dài thêm chút nếu phiếu vote cuối đến quá trễ, để mọi người còn kịp trở tay thay quần áo.

## Governor Votes

Từ đầu đến giờ chưa có extension nào cho sức mạnh vote, đây chính là giải pháp.

Sinh ra để hỗ trợ chuẩn token vote ERC5805 (có thể là ERC20 hay ERC721) và lấy đó làm con số tính sức mạnh vote cho từng đối tượng. Ngoài ra người dùng chuẩn token trên có thể delegate sức mạnh vote của mình cho người khác để có thể vote.

Không dừng lại ở đó extensions này cũng quy định luôn thời gian chuẩn (clock) tính theo Blocknumber để có sức mạnh vote (tránh flashloan lấy sức mạnh).

## Votes

Nếu token sử dụng trong vote không phải chuẩn ERC5805 thì sao? Thì xài contract này.

Về bản chất khi sử dụng contract này mặc dù có sẵn interface và logic tính toán sức mạnh vote. Nhưng phải định nghĩa sức mạnh vote tính sao. Nếu là ERC20 thì đơn giản là sức mạnh dựa vào balance, nhưng NFT thì phải định nghĩa rõ từng NFT sức mạnh sao.

Tóm lại đây là giải pháp thay thế của Governor Votes cho những token không có feature vote (ERC5805).
