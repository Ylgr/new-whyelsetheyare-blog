---
layout: blog
title: "Khai mở, thế giới NFT - Phần 1: EVM NFT - Chương 1: Sinh vật, nhà máy,
  cộng sự và hộp thần kỳ"
date: 2022-04-21T09:28:31.714Z
top_image: /images/uploads/47639788_p0_master1200.jpg
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
Theo dòng lịch sử loài người, từ thời các bộ lạc đầu tiên trên trái đất xuất hiện, song song cùng nhu cầu sinh tồn giữa cuộc sống tự nhiên đầy khắc nhiệt, con người đã bắt đầu có văn hóa, có ngôn ngữ và nghệ thuật. Theo dòng thời gian, nghệ thuật lưu truyền và cứ thế đến thời đại công nghiệp nơi bản quyền sáng tạo bắt đầu hình thành và dần chặt chẽ góp phần tạo môi trường cho giới nghệ sỹ phát triển khởi đầu từ các quốc gia Châu Âu như Áo Hung hay Italy.

"Art is fine food, great craftsmanship, and unrestrained passion."

"The language of music has no borders."

Đến thời hiện tại, Blockchain đã mang đến một món ăn mới cho giới nghệ sỹ đó là: NFT. Nói na ná đó là một dạng chứng minh quyền sở hữu của một người với một vật phẩm với toàn bộ mạng lưới Blockchain đó.

<!-- more -->

# 1. Khai mở thế giới: Biển mở

![](https://therecord.media/wp-content/uploads/2022/01/OpenSea-1280x720.jpg)

Biển mở (Opensea) là hệ sinh thái NFT nổi nhất trên Ethereum. Tại sao nó được nhắc đến ở đây. Bản chất khi làm việc trên hệ sinh thái EVM, mọi thứ đều (nên được) Opensource nên khác với môi trường phát triển phần mềm truyền thống, ta có thể dựa trên những source code của những sản phẩm đã thành công trên thị trường để phát triển thành sản phẩm của riêng mình.

## 1.1. Các thành phần của biển mở

Biển mở chia là hai đối tượng NFT chính là ERC721 và ERC1155. Nôm na là NFT duy nhất và NFT số lượng giới hạn đó, với đối tượng lại chia thành 2 cách dùng đó là vật phẩm và lootbox. Tóm lại là có 4 use case có thể sử dụng trong opensea.

![Cấu tạo của Opensea](/images/uploads/opensea.png "Cấu tạo của Opensea")

Về mặt smart contract, Opensea bao gồm 7 smart contract như hình. Nếu diễn tả theo use case thì ở mỗi đối tượng chỉ cần một contract creature/creature accessory là được use case sáng tác tác phẩm nghệ thuật, 2 use case còn lại cần 3 hoặc 4 smart contract như hình đã mô tả. Tóm lại 4 use case đó là:

1. NFT duy nhất.
2. NFT duy nhất bị giấu thuộc tính trong lootbox.
3. NFT số lượng giới hạn.
4. NFT số lượng giới hạn đặt trong các lootbox mở ra ngẫu nhiên.

### 1.2. Mô tả hoạt động

#### 1.2.1. NFT duy nhất

Bạn vừa tạo ra một bức tranh, giờ bạn cần bán nó. Hãy bán nó trên .... Opensea vì nó sẽ là duy nhất ... là NFT.

![](/images/uploads/copy-of-nft-creation.png)

User cần upload dữ liệu NFT lên Cloud và trả phí giao dịch, sau đó update lại uri của NFT nên smart contract.


#### 1.2.2. NFT duy nhất bị giấu thuộc tính trong lootbox

Giờ giả sử bạn có tạo một NFT, tuy nhiên bạn giấu thông tin thật của NFT đó để làm người nhạn bất ngờ 1 phen. Use case này sinh ra để phục vụ việc đó.

![](/images/uploads/copy-of-nft-creation-1-.png)

Gần như tương tự như use case 1 nhưng ở use case này thông tin được đẩy lên Cloud trước khi điền vào NFT, khi unpack NFT lootbox đó ra thì id sinh ra sẽ cần khớp với dữ liệu định sẵn trên Cloud sẽ trở thành món quà bất ngờ.

#### 1.2.3. NFT số lượng giới hạn

Giờ bạn là một idol, muốn bán ra một vài album có chữ ký riêng của bạn thì phải làm sao, use case này sẽ là dành cho bạn.

![](/images/uploads/copy-of-nft-creation-2-.png)

Khác với use case 1, khi upload dữ liệu lên có thể không cần cập nhật thông tin này lên Blockchain luôn mà chỉ cần khi có nhu cầu giao bán, ta mới "in" ra NFT đó với một số lượng hợp lý và treo lên sàn là được.

#### 1.2.4. NFT số lượng giới hạn đặt trong các lootbox mở ra ngẫu nhiên

Bạn có biết các tựa game gacha đình đám? Hay hỳ hục trong thế giới Battle Royal với những hòm mà không biết sẽ mở ra thứ gì. Use case này sinh ra với cơ chế hoạt động như vậy đó.

![](/images/uploads/copy-of-nft-creation-3-.png)

Nếu ai thường chơi game online thì chắc hẳn khá quen nhỉ. Dành cho những ai chưa rõ thì có nhiều item được đánh giá trị khác nhau, mỗi item đều là các NFT và được thiết kế qua những lootbox. Quản trị viên sẽ tiến hành setting thông số cho từng loại lootbox như số lượng vật phẩm mở ra, tỷ lệ từng vật phẩm hay tỷ lệ đảm bảo.
Điểm hay của cơ chế này là tính random theo Blockchain. Nghĩa là phụ thuộc vào thời điểm transaction được đưa vào Block và seed của người mở gần nhất. Nếu lượng người mở gần như liên tục thì việc cố tính xác suất gần như không thể, chưa kể còn tính ngẫu nghiên của việc transaction sẽ rơi và Block nào nữa.

# 2. Triển khai: Biển mở

Github: https://github.com/ProjectOpenSea/opensea-creatures

Đầu tiên cần clone repo, sau đó thì deploy lên. Tham khảo bài này nha: https://whyelsetheyare.com/2021/06/24/blockchain-thu%E1%BA%ADt-s%C6%B0-b%C6%B0%E1%BB%9Bc-2-thu%E1%BA%ADt-t%E1%BA%A1o-v%C3%A0ng/

Deploy thành công, ta sẽ có smart contract như setting ở hình cấu tạo của Opensea. 

Tạo một project ReactJs và bắt đầu thử nghịch nào!

Đầu tiên là khai báo biến contract:

```
  const [contract, setContract] = useState({
    creature: null,
    creatureFactory: null,
    creatureLootBox: null,
    creatureAccessory: null,
    lootBoxRandomness: null,
    creatureAccessoryLootBox: null,
    creatureAccessoryFactory: null,
  })
```

Và setup:

```
      setContract({
        creature: new web3.eth.Contract(CreatureAbi,creatureAddress),
        creatureFactory: new web3.eth.Contract(CreatureFactoryAbi,creatureFactoryAddress),
        creatureLootBox: new web3.eth.Contract(CreatureLootBoxAbi,creatureLootBoxAddress),
        creatureAccessory: new web3.eth.Contract(CreatureAccessoryAbi,creatureAccessoryAddress),
        lootBoxRandomness: new web3.eth.Contract(LootBoxRandomnessAbi,lootBoxRandomnessAddress),
        creatureAccessoryLootBox: new web3.eth.Contract(CreatureAccessoryLootBoxAbi,creatureAccessoryLootBoxAddress),
        creatureAccessoryFactory: new web3.eth.Contract(CreatureAccessoryFactoryAbi,creatureAccessoryFactoryAddress),
      })
```

Nếu là use case 1 và 3, việc sử dụng sẽ đơn giản là gọi hàm mint và setup thêm các thông tin cần thiết. Với setup full chức năng khi deploy thì quyền owner bây giờ bị chuyển cho factory nên use case 1 và 3 không còn khả dụng, chúng ta sẽ trực tiếp với use case 2 và 4.

Với use case 2, ta cần quan tâm tới các hàm:

* Mint NFT (với option 0 để tạo 1 NFT, option 1 để tạo nhiều NFT và option 2 để tạo lootbox)

`await contract.creatureFactory.methods.mint(option,address).send({from: currentAddress});`

* Unpack Lootbox (để công khai thuộc tính của NFT)

`await contract.creatureLootBox.methods.unpack(tokenID).send({from: currentAddress});`

Với use case 4, các hàm tương tự cần quan tâm:

`await contract.creatureAccessoryFactory.methods.mint(option,address, amount, "0x0").send({from: currentAddress});`

`await contract.creatureAccessoryLootBox.methods.unpack(id,currentAddress, 3).send({from: currentAddress});`

Lưu ý với use case 4, mặc định factory ko có quyền chuyển NFT được in ra tại địa chỉ deploy nên ta cần thêm 1 lệnh approve để có thể mint và unpack:

`await contract.creatureAccessory.methods.setApprovalForAll(creatureAccessoryFactoryAddress, true).send({from: currentAddress});`

Nay đến đây đã, bước tiếp theo chúng ta sẽ cùng tìm hiểu cách setup một sàn giao dịch để bán các NFT này và bí mật của chúng.
