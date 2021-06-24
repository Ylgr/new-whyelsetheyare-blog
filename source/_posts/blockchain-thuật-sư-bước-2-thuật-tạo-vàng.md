---
layout: blog
title: "Blockchain thuật sư - Bước 2: Thuật tạo vàng"
date: 2021-06-23T17:12:31.867Z
top_image: /images/uploads/71347093_p0.jpg
tags:
  - blockchain
  - crypto
  - lập trình
  - solidity
categories:
  - Lập trình
---
*"Điều đơn giản nhất cũng là những điều phi thường nhất và chỉ những người thông thái nhất mới có thể tìm thấy chúng."*

Câu chuyện kể về ở một vương quốc nọ tên là Nift, một nơi và đã từng có quãng thời gian, đây là một đất nước của tự do, giàu có và hạnh phúc. Dần theo thời gian, con người nơi đây dần quên mất cuộc sống này và rồi bị cám dỗ bởi sự tham lam, ghen ghét và đố kỵ. Có một nhà giả kim nọ nơi đây mang biệt danh Toái Nguyệt không muốn câu chuyện của thành phố kết thúc như vậy.

<!-- more -->

# 1. Quá trình nghiên cứu

## 1.1. Giá trị hóa ký ức

![](/images/uploads/76405513_p0.jpg)

Nhà giả kim tiến vào bên chiếc nồi chế quen thuộc [Remix](https://remix.ethereum.org/), bắt đầu tỉ mỉ chế ra 1000 đơn vị Nift memory dust (ERC20 token). Đây là công thức chế tạo:

```
// SPDX-License-Identifier: MIT

pragma solidity ^0.8.0;

import "https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.1.0/contracts/token/ERC20/ERC20.sol";

contract NiftMemoryDust is ERC20 {
    
    constructor() ERC20("Nift memory dust", "NIFT-DUST") {
        _mint(msg.sender,1000 * 1e18);
    }
}
```

Bằng cách đưa công thức vào một file .sol tiến hành compile và deploy, bụp một nghìn "bụi ký ức Nift" đã được tạo ra trong ống nghiệm.

Giải thích: Đây chính là cách để tạo ra token ERC20 trên các mạng lưới hỗ trợ EVM.

## 1.2. Gửi gắm giá trị vào các bảo vật linh hồn

![](/images/uploads/nift-memory-treasury.png)

Cất ống nghiệm một sang một bên, ngài đưa mở hộp và thả vào nồi nấu một vài loại hợp chất để tạo ra: Bông hoa của sự tư do, chiếc lá của sự giàu có và giọt nước của sự hạnh phúc.

```
// SPDX-License-Identifier: MIT

pragma solidity ^0.8.0;

import "https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.1.0/contracts/token/ERC721/extensions/ERC721URIStorage.sol";

contract NiftMemoryDust is ERC721URIStorage {
    
    constructor() ERC721("Nift memory treasury", "NIFT-TREASURY") {
        _mint(msg.sender,1);
        _mint(msg.sender,2);
        _mint(msg.sender,3);
        
        _setTokenURI(1, "https://ylgr.github.io/nift-memory/treasury/freedom.json");
        _setTokenURI(2, "https://ylgr.github.io/nift-memory/treasury/wealth.json");
        _setTokenURI(3, "https://ylgr.github.io/nift-memory/treasury/happiness.json");
    }
}
```
Giải thích: Smart contract trên tạo ra contract token ERC721 (NFT) gồm 3 token có id tương ứng 1, 2, 3. Mỗi id gắn với một thông tin URI như trong source code.

# 2. Đóng gói và tạo hình

Sau khi hoàn thành và chạy thử thành công smart contract trên remix, giờ ta sẽ mang chúng setup lại trên truffle để thuận tiện trong việc build deploy data, abi và verify network.

Trong phần này chúng ta sẽ sử dụng Truffle để triển khai Smart contract và React để làm frontend hiển thị thành quả.

Note: Bạn cần cài đặt [Node.js](https://nodejs.org/en/download/package-manager/) và [Truffle](https://www.trufflesuite.com/docs/truffle/getting-started/installation) để có thể tiến hành.

Đầu tiên ta khởi tạo project bằng cách [unbox template](https://www.trufflesuite.com/boxes/react).

```
mkdir nift-memory
cd nift-memory
truffle unbox react 
```
Khởi tạo npm và thêm 1 vài dependency cần thiết cho việc dev.
```
npm init
npm install @openzeppelin/contracts
npm install @truffle/hdwallet-provider
npm install dotenv
npm install truffle-plugin-verify --save-dev
```
Tạo file .env tại root của project và truyền giá trị PRIVATE_KEY và BSCSCANAPIKEY (sử dụng cho verify contract). Sau đó setup lại config trong file: truffle-config.js
```
const path = require("path");
const HDWalletProvider = require('@truffle/hdwallet-provider');
require('dotenv').config();

const privateKey = process.env.PRIVATE_KEY

module.exports = {
  // See <http://truffleframework.com/docs/advanced/configuration>
  // to customize your Truffle configuration!
  contracts_build_directory: path.join(__dirname, "client/src/contracts"),
  plugins: [
    'truffle-plugin-verify'
  ],
  api_keys: {
    bscscan: process.env.BSCSCANAPIKEY,
    testnet: process.env.BSCSCANAPIKEY,
  },
  networks: {
    development: {
      host: "127.0.0.1",     // Localhost (default: none)
      port: 8545,            // Standard BSC port (default: none)
      network_id: "*",       // Any network (default: none)
    },
    testnet: {
      provider: () => new HDWalletProvider(privateKey, `https://data-seed-prebsc-1-s1.binance.org:8545`),
      network_id: 97,
      confirmations: 10,
      timeoutBlocks: 200,
      skipDryRun: true
    },
    bsc: {
      provider: () => new HDWalletProvider(privateKey, `https://bsc-dataseed1.binance.org`),
      network_id: 56,
      confirmations: 10,
      timeoutBlocks: 200,
      skipDryRun: true
    },
  },

  // Set default mocha options here, use special reporters etc.
  mocha: {
    // timeout: 100000
  },

  // Configure your compilers
  compilers: {
    solc: {
      version: "^0.8.4", // A version or constraint - Ex. "^0.5.0"
    }
  }
};

```


# 3. Hiện thực hóa