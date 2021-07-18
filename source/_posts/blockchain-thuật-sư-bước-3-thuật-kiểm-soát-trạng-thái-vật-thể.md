---
layout: blog
title: "Blockchain thuật sư - Bước 3: Thuật kiểm soát trạng thái vật thể"
date: 2021-07-04T02:02:48.663Z
top_image: /images/uploads/81566459_p0.jpg
tags:
  - blockchain
  - crypto
  - develop
categories:
  - Lập trình
---
*"Vào bất kỳ thời điểm nào trong cuộc đời, mỗi người đều có khả năng thực hiện những gì họ mơ ước."*

Tiếp nối câu chuyện hôm nọ, những báu vật mà nhà giả kim nọ không chỉ dừng lại ở việc quyền sở hữu, mà nó còn khả năng gắn kết lại thành trái tim của Nift để hồi sinh sự sống tại đây. Câu truyện xin được tiếp tục.

<!-- more -->

# 1. Trái tim của Nift

Những báu vật và bụi giả kim kim kia không đơn giảm là những linh vật vô tri chỉ có ý nghĩa tượng chưng. Vị giả kim sử dụng một niệm thuật khắc cổ ngữ lên những linh vật đó và khởi động một hiệp ước để chúng liên kết với nhau tạo thành một thứ sức mạnh để cứu lấy vương quốc Nift.

```solidity
// SPDX-License-Identifier: MIT

pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC721/extensions/ERC721URIStorage.sol";
import "@openzeppelin/contracts/token/ERC721/extensions/ERC721URIStorage.sol";
import "@openzeppelin/contracts/access/Ownable.sol";
import "@openzeppelin/contracts/token/ERC20/IERC20.sol";
import "@openzeppelin/contracts/token/ERC721/IERC721.sol";
import "@openzeppelin/contracts/utils/math/SafeMath.sol";

contract NiftMemoryHeart is ERC721URIStorage, Ownable {

    constructor() ERC721("Nift memory heart", "NIFT-HEART") {}

    IERC20 dust = IERC20(0xaae5fc57aE9B2702e165224bc7b4f700ba698b22);
    IERC721 treasure = IERC721(0xE3864Fb24851EA437043Ae62104dF4692e11B8b1);

    uint8 tokenId = 99;

    event Craft(address addr, uint256 time);
    event Revert(address addr, uint256 time);
    event WithdrawDust(uint256 amount, address receiver, uint256 time);

    function craft() public {
        treasure.transferFrom(msg.sender, address(this), 1);
        treasure.transferFrom(msg.sender, address(this), 2);
        treasure.transferFrom(msg.sender, address(this), 3);

        dust.transferFrom(msg.sender, address(this), 100 * 1e18);

        _mint(msg.sender,tokenId);

        _setTokenURI(tokenId, "https://ylgr.github.io/nift-memory/heart/heart.json");

        emit Craft(msg.sender, block.timestamp);
    }

    function revert() public {
        require(ownerOf(tokenId) == msg.sender, "Not own heart");
        _burn(tokenId);

        treasure.transferFrom(address(this), msg.sender, 1);
        treasure.transferFrom(address(this), msg.sender, 2);
        treasure.transferFrom(address(this), msg.sender, 3);

        emit Revert(msg.sender, block.timestamp);
    }

    function withdrawDust() public onlyOwner {
        uint256 amount = dust.balanceOf(address(this));

        require(
            amount > 0,
            "Token insufficient"
        );

        require(
            dust.transfer(owner(), amount),
            "Token transfer fail"
        );

        emit WithdrawDust(
            amount,
            owner(),
            block.timestamp
        );
    }


}

```

Giải thích: Smart contract khởi tạo một NFT khác nhưng không init từ đầu mà được "mint" qua function craft khi người dùng sở hữu cả 3 NFT của bước 2. Function revert cho phép người dùng quay ngược quá trình này để tạo trở lại thành 3 loại NFT cũ và "burn" NFT mới đi. Function withdrawDust làm nhiệm vụ như tên gọi của nó, hãy tưởng tượng contract này là shop của bạn thì hàm này đóng vai trò rút tiền trong shop.

Viết ấn chú xong, ta tạo file migration:

```javascript
const NiftMemoryHeart = artifacts.require("./NiftMemoryHeart.sol");

module.exports = function(deployer) {
  deployer.deploy(NiftMemoryHeart);
};
```

Sau đó deploy và migrate contract:

```shell
truffle migrate --network testnet
truffle run verify NiftMemoryHeart@0x5175EBC5503acE38860821365b37Ac58b7BB624c --network testnet

```

Và ta-da, contract đã được hiện thực hóa: https://testnet.bscscan.com/address/0x5175EBC5503acE38860821365b37Ac58b7BB624

# 2. Chế tạo cùng phân giải, đưa chúng vào cùng phong ấn

Dù rằng với nhiêu kia, ta đã có thể thao tác chế tạo hay phân giải Nift Heart, ta vẫn cần một interface để dễ dàng sử dụng bởi bất kỳ ai. Quay lại với client