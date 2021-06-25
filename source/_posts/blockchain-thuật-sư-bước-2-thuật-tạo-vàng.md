---
layout: blog
title: "Blockchain thuật sư - Bước 2: Thuật tạo vàng"
date: 2021-06-24T02:22:28.117Z
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

```solidity
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

```solidity
// SPDX-License-Identifier: MIT

pragma solidity ^0.8.0;

import "https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.1.0/contracts/token/ERC721/extensions/ERC721URIStorage.sol";

contract NiftMemoryTreasure is ERC721URIStorage {
    
    constructor() ERC721("Nift memory treasure", "NIFT-TREASURE") {
        _mint(msg.sender,1);
        _mint(msg.sender,2);
        _mint(msg.sender,3);
        
        _setTokenURI(1, "https://ylgr.github.io/nift-memory/treasure/freedom.json");
        _setTokenURI(2, "https://ylgr.github.io/nift-memory/treasure/wealth.json");
        _setTokenURI(3, "https://ylgr.github.io/nift-memory/treasure/happiness.json");
    }
}
```

Giải thích: Smart contract trên tạo ra contract token ERC721 (NFT) gồm 3 token có id tương ứng 1, 2, 3. Mỗi id gắn với một thông tin URI như trong source code.

# 2. Đóng gói và tạo hình

Sau khi hoàn thành và chạy thử thành công smart contract trên remix, giờ ta sẽ mang chúng setup lại trên truffle để thuận tiện trong việc build deploy data, abi và verify network.

Trong phần này chúng ta sẽ sử dụng Truffle để triển khai Smart contract và React để làm frontend hiển thị thành quả.

Note: Bạn cần cài đặt [Node.js](https://nodejs.org/en/download/package-manager/) và [Truffle](https://www.trufflesuite.com/docs/truffle/getting-started/installation) để có thể tiến hành.

Đầu tiên ta khởi tạo project bằng cách [unbox template](https://www.trufflesuite.com/boxes/react).

```shell
mkdir nift-memory
cd nift-memory
truffle unbox react 
```

Khởi tạo npm và thêm 1 vài dependency cần thiết cho việc dev.

```shell
npm init
npm install @openzeppelin/contracts
npm install @truffle/hdwallet-provider
npm install dotenv
npm install truffle-plugin-verify --save-dev
```

Tạo file .env tại root của project và truyền giá trị PRIVATE_KEY và BSCSCANAPIKEY (sử dụng cho verify contract). Sau đó setup lại config trong file: truffle-config.js

```javascript
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

Xóa tất cả các file có sẵn ở contracts, migrations và test, sau đó tạo 2 file NiftMemoryDust.sol và NiftMemoryTreasure.sol tương ứng trong thư mục contracts.

Chuyển code sang và thay đổi lại cấu trúc import của mỗi file, thay đoạn `https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.1.0` thành `@openzeppelin`.

Tạo file 1_deploy_contract.js trong migrations và thêm code deploy:

```javascript
const NiftMemoryDust = artifacts.require("./NiftMemoryDust.sol");
const NiftMemoryTreasure = artifacts.require("./NiftMemoryTreasure.sol");

module.exports = function(deployer) {
  deployer.deploy(NiftMemoryDust);
  deployer.deploy(NiftMemoryTreasure);
};
```

Và done, phần setup đã xong.

Giờ ta sẽ triển khai deploy smart contract này lên binance smart chain testnet và verify nó.

Đầu tiên ta cần [faucet BNB](https://testnet.binance.org/faucet-smart). Khi đã có BNB và .env đã setup đẩy đủ thông tin.

```shell
truffle migrate --network testnet
```

Chờ script chạy xong và ta-da, Dust và Treasure đã được đẩy lên binance smart chain testnet.

NiftMemoryDust: https://testnet.bscscan.com/address/0xaae5fc57ae9b2702e165224bc7b4f700ba698b22
NiftMemoryTreasure: https://testnet.bscscan.com/address/0xe3864fb24851ea437043ae62104df4692e11b8b1

Tuy nhiên smart contract này chưa được verify nên source code còn tồn tại dạng byte code, ta cần thêm 1 bước verify nữa trước khi sử dụng.

```shell
truffle run verify NiftMemoryDust@0xaae5fc57ae9b2702e165224bc7b4f700ba698b22 --network testnet
truffle run verify NiftMemoryTreasure@0xe3864fb24851ea437043ae62104df4692e11b8b1 --network testnet
```

Xong! Giờ đã có hai smart contract này chạy trên binance smart chain testnet. Bước tiếp theo chúng ta sẽ viết giao diện hiển thị thông tin 2 loại token này.

# 3. Hiện thực hóa

Tiếp đến ta sẽ sử dụng React có sẵn khi unbox để dựng giao diện hiển thị. Vào thư mục client xóa hết những file không cần thiết cho project: App.css, App.js, App.test.js, index.css.

Setting lại package.json

```json
{
  "name": "client",
  "version": "0.1.0",
  "private": true,
  "dependencies": {
    "axios": "^0.21.1",
    "bootstrap": "^5.0.2",
    "react": "16.11.0",
    "react-dom": "16.11.0",
    "react-scripts": "3.2.0",
    "reactstrap": "^8.9.0",
    "web3": "1.2.2"
  },
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject",
    "deploy": "gh-pages -d build"
  },
  "eslintConfig": {
    "extends": "react-app"
  },
  "browserslist": {
    "production": [
      ">0.2%",
      "not dead",
      "not op_mini all"
    ],
    "development": [
      "last 1 chrome version",
      "last 1 firefox version",
      "last 1 safari version"
    ]
  },
  "devDependencies": {
    "gh-pages": "^3.2.3"
  },
  "homepage": "https://ylgr.github.io/nift-memory/"
}
```

Lưu ý: thông tin homepage cần sửa lại theo thông tin project của bạn.

Nhắc lệnh vào client và cài đặt những dependency cần thiết:

```shell
cd client
npm install
```

Đưa dữ liệu treasure vào thư mục public.

![](/images/uploads/screenshot-from-2021-06-24-23-19-07.png)

Import bootstrap vào index.js

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import 'bootstrap/dist/css/bootstrap.min.css';
import App from './App';
import * as serviceWorker from './serviceWorker';

ReactDOM.render(<App />, document.getElementById('root'));

// If you want your app to work offline and load faster, you can change
// unregister() to register() below. Note this comes with some pitfalls.
// Learn more about service workers: https://bit.ly/CRA-PWA
serviceWorker.unregister();
```

Tạo lại file App.js và code:

```javascript
import React, {Component} from "react";
import NiftMemoryDust from "./contracts/NiftMemoryDust.json";
import NiftMemoryTreasure from "./contracts/NiftMemoryTreasure.json";
import Web3 from "web3";
import {
    Card, Button, CardImg, CardTitle, CardText,
    CardSubtitle, CardBody, Col, Container, Row
} from 'reactstrap';
import Axios from "axios";

class App extends Component {
    state = {web3: null, dustContract: null, dustInfo: {}, treasureContract: null, treasureInfo: []};

    componentDidMount = async () => {
        try {
            // Get network provider and web3 instance.
            const web3 = new Web3('https://data-seed-prebsc-1-s1.binance.org:8545')

            const networkId = await web3.eth.net.getId()
            const dustContract = new web3.eth.Contract(NiftMemoryDust.abi, NiftMemoryDust.networks[networkId].address)

            const dustInfo = {
                name: await dustContract.methods.name().call(),
                symbol: await dustContract.methods.symbol().call(),
                totalSupply: (await dustContract.methods.totalSupply().call())/10e18
            }

            const treasureContract = new web3.eth.Contract(NiftMemoryTreasure.abi, NiftMemoryTreasure.networks[networkId].address)

            let treasureInfo = []
            for(let tokenId = 1; tokenId <= 3; tokenId++) {
                const uri = await treasureContract.methods.tokenURI(tokenId).call()
                const response = await Axios(uri)
                response.data.owner = await treasureContract.methods.ownerOf(tokenId).call()
                treasureInfo.push(response.data)
            }
            this.setState({web3, dustContract, dustInfo, treasureContract, treasureInfo})
        } catch (error) {
            // Catch any errors for any of the above operations.
            alert(
                `Failed to load web3. Check console for details.`,
            );
            console.error(error);
        }
    };

    render() {
        return (
            <div className="App">
                <Container>
                    <Card>
                        <CardText>Name: {this.state.dustInfo.name}</CardText>
                        <CardText>Symbol: {this.state.dustInfo.symbol}</CardText>
                        <CardText>Total supply: {this.state.dustInfo.totalSupply}</CardText>
                    </Card>
                </Container>
                <Row>
                    {this.state.treasureInfo.map((e,index) => (
                        <Col md="4" key={index}>
                            <Card>
                                <CardImg height="750px" top src={e.image} alt={e.name}/>
                                <CardBody>
                                    <CardTitle>{e.name}</CardTitle>
                                    <CardSubtitle>Owner: {e.owner}</CardSubtitle>
                                    <CardText>{e.description}</CardText>
                                </CardBody>
                            </Card>
                        </Col>
                    ))}


                </Row>

            </div>
        );
    }
}

export default App;
```

Build và deploy lên github-page:

```shell
npm run build
npm run deploy
```

Kết quả:

![](/images/uploads/screenshot-from-2021-06-24-23-09-57.png)

Website thực tế từ bước 2 đến bước 4 của seri này: https://ylgr.github.io/nift-memory/