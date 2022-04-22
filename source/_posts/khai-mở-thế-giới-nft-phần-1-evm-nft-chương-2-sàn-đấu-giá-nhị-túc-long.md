---
layout: blog
title: "Khai mở, thế giới NFT - Phần 1: EVM NFT - Chương 2: Sàn đấu Nhị Túc Long"
date: 2022-04-22T03:33:44.030Z
top_image: /images/uploads/52873218_p0.jpg
tags:
  - nft
  - solidity
  - evm
  - smartcontract
  - code
categories:
  - Lập trình
  - NFT
---
Nghệ thuật là một niềm cảm hứng bất tận nhưng cũng cần rất nhiều tâm huyết và nỗ lực cho nó. Trong quá khứ, nhiều họa sỹ lừng danh mà tên tuổi và tác phẩm của họ vẫn còn vang danh đến tận bây giờ nhưng khi còn sống họ phải đối mặt với vấn đề tài chính và chết đi trong nghèo khó và bệnh tật. 

Ngày nay công nghệ thông tin đạt bước tiến vượt bậc khiến các tác phẩm nghệ thuật dễ dàng hơn đến tay độc giả muốn sở hữu chúng và cùng với Blockchain và NFT. Những tác phẩm này giờ có thể giao bán mà không cần đến sự có mặt của bên thứ ba, các quyền lợi bản quyền giờ cũng dễ dàng được trao đến tay người nghệ sỹ mà không cần đến mối quan hệ phức tạp của pháp luật.

Điều đáng nói là việc hợp pháp hóa các cuộc đấu giá nghệ thuật từ trước đến giờ chưa bao giờ đơn giản đến thế. 

Nghệ sỹ vui.

Người mua vui.

Người bán vui.

Cộng đồng Blockchain vui.

<!-- more -->

# 1. Hệ sinh thái Nhị Túc Long

![](https://media.githubusercontent.com/media/ProjectWyvern/wyvern-branding/master/logo/logo-square-red-transparent-200x200.png?raw=true)

Nhị Túc Long - Wyvern Ethereum (từ giờ sẽ gọi là WE cho ngắn) gồm nhiều contract bao quanh concept chính: sàn giao dịch tài sản mã hóa phi tập trung.

## 1. Proxy registry

Có một điểm đặc biệt trong Smart contract của Opensea mà chương trước chưa đề cập, đó khi deploy smart contract NFT, bạn sẽ cần điền một địa chỉ để sử dụng gọi là proxy address. Địa chỉ này chính là địa chỉ của smart contract Wyvern Proxy Registry này. Nói cách khác smart contract cần được deploy trước cả smart contract của Opensea rồi mới sử dụng địa chỉ deploy thành công đó điền vào bước migrate của smart contract Opensea. Bản chất địa chỉ proxy đó là địa chỉ có quyền transfer trực tiếp tài sản NFT của Opensea mà không cần thông qua cơ chế Approve nhằm tiện và linh hoạt hơn cho việc giao dịch phi tập trung.

Về mặt contract thì sau khi deploy xong contract Opensea thì chạy thêm function `grantInitialAuthentication` để địa chỉ contract được đánh dấu và giao dịch.

## 2. Token transfer proxy

Mỗi một định dạng token có một function transfer khác nhau và để thống nhất cách dùng với toàn bộ các định dạng hiện có thì đó là lý do cần sử dụng smart contract này để phục vụ nhu cầu đó.

Về mặc định, smart contract này gắn liền với proxy registry để tiến hành trigger giao dịch tài sản mã hóa. Tuy nhiên không phải token nào cũng có setup approve mặc định cho proxy registry, khi vào trường hợp này yêu cần cần thiết là tiến hành approve cho smart contract này có quyền giao dịch.

## 3. Exchange core

Trung tâm của WE là sàn giao dịch tài sản mã hóa. Tại đây, contract đã được setting khá đầy đủ thông số cho nhiều trường hợp. Hỗ trợ cả native token lẫn các loại token khác, hỗ trợ cả phương thức bán fixed giá và đấu giá Hà Lan, hỗ trợ cả ngàn lẻ một tiện ích khác mà phải làm viêc trực tiếp với WE mới có cơ hội tìm hiểu thêm.

## 4. Others

Ở những thành phần lặt vặt còn lại không được hướng dẫn bên dưới sẽ được liệu kê lan man tại đây, chúng ta có:

- Token WE: được implement cơ chế xử lý NFT, cơ chế deplay release và burnable.
- DAO: Khi tương tác với tài sản mã hóa có một tùy chọn là tài sản sau khi giao dịch sẽ được giao lại cho DAO nắm giữ và quyết định, từ đó tạo sự công bằng cho những NFT được tham gia bởi nhiều người.
- Upgradeable proxy: Phòng cả trường hợp xấu nhất, contract có thể tự nâng cấp mà vẫn giữ được địa chỉ cũ đang chạy và dữ liệu bằng cách bố trí một tầng riêng biệt chứa data và trỏ đến tầng chứa logic.

# 2. Ứng dụng WE để giao dịch NFT Opensea

![](https://static.opensea.io/og-images/Metadata-Image.png)

Github repo: https://github.com/ProjectWyvern/wyvern-ethereum

Bản thân WE có khá nhiều lệnh deploy, trong kịch bản ứng dụng với Opensea thì chỉ cần file migrate thứ 5: `5_deploy_registry_and_exchange.js`

Trong kịch bản sử dụng ở bài viết này, chúng ta sẽ lấy ví dụ là chúng ta cần bán NFT ra 1 loại token khác có tên là Nift memory dust (NIFT-DUST) mà chúng ta đã tạo ở bước 2 của thuật giả kim ở điều kiện bán là fixed giá.

Đầu tiên ta cần setup smart contract như đã làm ở bài viết trước:

```
  const [contract, setContract] = useState({
    wyvernExchange: null,
    wyvernProxyRegistry: null,
    wyvernTokenTransferProxy: null,
    dust: null,
  })

```

```
      setContract({
        wyvernExchange: new web3.eth.Contract(WyvernExchangeAbi, wyvernExchangeAddress),
        wyvernProxyRegistry: new web3.eth.Contract(WyvernProxyRegistryAbi, wyvernRegistryProxyAddress),
        wyvernTokenTransferProxy: new web3.eth.Contract(WyvernTokenTransferProxyAbi, wyvernTokenTransferProxyAddress),
        dust: new web3.eth.Contract(DustAbi, dustAddress)
      })
```

Ở lần đầu sử dụng, chúng ta cần tạo authorite cho Proxy registry (lần đầu khi sử dụng sàn):

```await contract.wyvernProxyRegistry.methods.grantInitialAuthentication(wyvernExchangeAddress).send({from: currentAddress})```

Sau đó tạo proxy cho chính địa chỉ sử dụng sàn (lần đầu khi dùng một địa chỉ bất kỳ thao tác):
```await contract.wyvernProxyRegistry.methods.registerProxy().send({from: currentAddress})```

Setup template tạo order:
```
  const makeOrder = async (exchange, isMaker) => ({
    exchange: exchange,
    maker: currentAddress,
    taker: currentAddress,
    makerRelayerFee: 0,
    takerRelayerFee: 0,
    makerProtocolFee: 0,
    takerProtocolFee: 0,
    feeRecipient: isMaker ? currentAddress : '0x0000000000000000000000000000000000000000',
    feeMethod: 0,
    side: 0,
    saleKind: 0,
    target: await contract.wyvernProxyRegistry.methods.proxies(currentAddress).call(),
    howToCall: 0,
    calldata: '0x',
    replacementPattern: '0x',
    staticTarget: '0x0000000000000000000000000000000000000000',
    staticExtradata: '0x',
    paymentToken: currentAddress,
    basePrice: new BigNumber(0).toString(),
    extra: 0,
    listingTime: 0,
    expirationTime: 0,
    salt: new BigNumber(1).toString()
  })
```

Chuẩn bị schema bằng lib `wyvern-schemas`:

```
import * as WyvernSchemas from 'wyvern-schemas';

  const _getSchema = (schemaName_) => {
    const schema = WyvernSchemas.schemas['main'].filter(
        (s) => s.name == schemaName_
    )[0];

    if (!schema) {
      throw new Error(
          `Trading for this asset (${schemaName_}) is not yet supported. Please contact us or check back later!`
      );
    }
    return schema;
  }
```

Đặc điểm của Wyvern-ethereum là khi thực hiện giao dịch đăng bán, người đăng bán không nhất thiết cần phải đăng giao dịch lên Blockchain (chỉ với dạng bán fixed giá). WE sử dụng cơ chế là người bán chỉ cần submit chữ ký là đã đặt lệnh bán lên, người mua sẽ submit chữ kí này cùng lệnh automaticOrder của họ là tự khớp được, điều này giúp đỡ phần phí giao dịch và có thể dùng backend để lưu chữ ký của người bán qua một dịch vụ trung gian được, đó là thứ mà Opensea đã làm: đứng ra làm trung gian.

Ta cần chuẩn bị thêm hàm hash order nữa:

```
  const hashOrder = (order) => {
    return Web3.utils.soliditySha3(
        {type: 'address', value: order.exchange},
        {type: 'address', value: order.maker},
        {type: 'address', value: order.taker},
        {type: 'uint', value: new BigNumber(order.makerRelayerFee)},
        {type: 'uint', value: new BigNumber(order.takerRelayerFee)},
        {type: 'uint', value: new BigNumber(order.takerProtocolFee)},
        {type: 'uint', value: new BigNumber(order.takerProtocolFee)},
        {type: 'address', value: order.feeRecipient},
        {type: 'uint8', value: order.feeMethod},
        {type: 'uint8', value: order.side},
        {type: 'uint8', value: order.saleKind},
        {type: 'address', value: order.target},
        {type: 'uint8', value: order.howToCall},
        {type: 'bytes', value: order.calldata},
        {type: 'bytes', value: order.replacementPattern},
        {type: 'address', value: order.staticTarget},
        {type: 'bytes', value: order.staticExtradata},
        {type: 'address', value: order.paymentToken},
        {type: 'uint', value: new BigNumber(order.basePrice)},
        {type: 'uint', value: new BigNumber(order.extra)},
        {type: 'uint', value: new BigNumber(order.listingTime)},
        {type: 'uint', value: new BigNumber(order.expirationTime)},
        {type: 'uint', value: order.salt}
    ).toString('hex')
  }
```


Phù, giờ coi như xong bước chuẩn bị, giờ hãy thử giao dịch NFT đầu tiên nào:

Tạo order:


```
    let buy = await makeOrder(wyvernExchangeAddress, false)
    let sell = await makeOrder(wyvernExchangeAddress, true)
    sell.side = 1
    buy.feeMethod = 1
    sell.feeMethod = 1
    buy.paymentToken = dustAddress
    sell.paymentToken = dustAddress
    buy.basePrice = new BigNumber(10000).toString()
    sell.basePrice = new BigNumber(10000).toString()
    sell.makerProtocolFee = new BigNumber(100).toString()
    sell.makerRelayerFee = new BigNumber(100).toString()
```

Setup thông tin vật phẩm bán:

```
import {encodeBuy, encodeSell} from "wyvern-schemas";

    const schema = _getSchema('ERC721')
    const sellSpec = encodeSell(
        schema,
        {address: creatureAddress, id: '1'},
        currentAddress,
    )
    const buySpec = encodeBuy(
        schema,
        {address: creatureAddress, id: '1'},
        currentAddress,
    );

    buy.calldata = buySpec.calldata
    buy.replacementPattern = buySpec.replacementPattern
    buy.target = buySpec.target

    sell.calldata = sellSpec.calldata
    sell.replacementPattern = sellSpec.replacementPattern
    sell.target = sellSpec.target
```

Approve cho token sử dụng giao dịch và check lại xem có match giao dịch không: 
```

    const allowance = await contract.dust.methods.allowance(currentAddress, wyvernTokenTransferProxyAddress).call()
    console.log('allowance: ', allowance);
    if(allowance == 0) {
      await contract.dust.methods.approve(wyvernTokenTransferProxyAddress, '0xffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff').send({from: currentAddress});
    }

    const canOderMatch = await contract.wyvernExchange.methods.ordersCanMatch_(
        [buy.exchange, buy.maker, buy.taker, buy.feeRecipient, buy.target, buy.staticTarget, buy.paymentToken, sell.exchange, sell.maker, sell.taker, sell.feeRecipient, sell.target, sell.staticTarget, sell.paymentToken],
        [buy.makerRelayerFee, buy.takerRelayerFee, buy.makerProtocolFee, buy.takerProtocolFee, buy.basePrice, buy.extra, buy.listingTime, buy.expirationTime, buy.salt, sell.makerRelayerFee, sell.takerRelayerFee, sell.makerProtocolFee, sell.takerProtocolFee, sell.basePrice, sell.extra, sell.listingTime, sell.expirationTime, sell.salt],
        [buy.feeMethod, buy.side, buy.saleKind, buy.howToCall, sell.feeMethod, sell.side, sell.saleKind, sell.howToCall],
        buy.calldata,
        sell.calldata,
        buy.replacementPattern,
        sell.replacementPattern,
        buy.staticExtradata,
        sell.staticExtradata
    ).call();
    console.log('canOderMatch: ', canOderMatch);
```

Hash order:

```
    const buyHash = hashOrder(buy)
    const sellHash = hashOrder(sell)

    let buySignature = await web3.eth.sign(buyHash, currentAddress)
    buySignature = buySignature.substr(2)
    const br = '0x' + buySignature.slice(0, 64)
    const bs = '0x' + buySignature.slice(64, 128)
    const bv = 27 + parseInt('0x' + buySignature.slice(128, 130), 16)
    let sellSignature = await web3.eth.sign(sellHash, currentAddress)
    sellSignature = sellSignature.substr(2)
    const sr = '0x' + sellSignature.slice(0, 64)
    const ss = '0x' + sellSignature.slice(64, 128)
    const sv = 27 + parseInt('0x' + sellSignature.slice(128, 130), 16)
```

Cuối cùng là lệnh match order:
```
await contract.wyvernExchange.methods.atomicMatch_(
        [buy.exchange, buy.maker, buy.taker, buy.feeRecipient, buy.target, buy.staticTarget, buy.paymentToken, sell.exchange, sell.maker, sell.taker, sell.feeRecipient, sell.target, sell.staticTarget, sell.paymentToken],
        [buy.makerRelayerFee, buy.takerRelayerFee, buy.makerProtocolFee, buy.takerProtocolFee, buy.basePrice, buy.extra, buy.listingTime, buy.expirationTime, buy.salt, sell.makerRelayerFee, sell.takerRelayerFee, sell.makerProtocolFee, sell.takerProtocolFee, sell.basePrice, sell.extra, sell.listingTime, sell.expirationTime, sell.salt],
        [buy.feeMethod, buy.side, buy.saleKind, buy.howToCall, sell.feeMethod, sell.side, sell.saleKind, sell.howToCall],
        buy.calldata,
        sell.calldata,
        buy.replacementPattern,
        sell.replacementPattern,
        buy.staticExtradata,
        sell.staticExtradata,
        [bv, sv],
        [br, bs, sr, ss, '0x0000000000000000000000000000000000000000000000000000000000000000']
    ).send({from: currentAddress})
```

P/S: Còn về vụ bán kiểu đấu giá Hà Lan thì bạn buộc phải thêm một hàm approve cho mua nữa (tất nhiên thông số setup sẽ khác đi):

```
await contract.wyvernExchange.methods.approveOrder_(
        [buy.exchange, buy.maker, buy.taker, buy.feeRecipient, buy.target, buy.staticTarget, buy.paymentToken],
        [buy.makerRelayerFee, buy.takerRelayerFee, buy.makerProtocolFee, buy.takerProtocolFee, buy.basePrice, buy.extra, buy.listingTime, buy.expirationTime, buy.salt],
        buy.feeMethod,
        buy.side,
        buy.saleKind,
        buy.howToCall,
        buy.calldata,
        buy.replacementPattern,
        buy.staticExtradata,
        true
    ).send({from: currentAddress})
```

Và câu chuyện NFT trên hệ sinh thái EVM xin được khép lại ở đây. Bài viết tiếp theo của series này sẽ "có thể" là miền đất hứa của NFT thời điểm hiện tại: hệ sinh thái Solana.