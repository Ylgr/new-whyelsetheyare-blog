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

Bây giờ kịch bản thế này nha, chúng ta có 4 ví bao gồm: 

* Ví master chịu trách nhiệm quả lý token, in thêm token, ...
* Ví fee payer: Ví duy nhất chứ SOL chịu bất kỳ khoản phí giao dịch nào xảy ra trong hệ thống.
* Ví user 1.
* Ví user 2.

Chúng ta sẽ tạo một đồng token mới và các user chỉ cần dùng đồng token đó (tạm gọi là bic) cho phí giao dịch thôi.

***Giờ thì bắt đầu nào.***

Setup lib:

```
import {Col, Row, Label, Button, Collapse, Card, CardBody, CardText, CardTitle, CardLink, Input} from 'reactstrap';
import {web3, Wallet, BN} from '@project-serum/anchor';
import Base58 from 'base-58';
import { TOKEN_PROGRAM_ID, Token, u64, ASSOCIATED_TOKEN_PROGRAM_ID, NATIVE_MINT, AccountLayout, MintLayout } from "@solana/spl-token";
import {
    Keypair,
    SystemProgram,
} from '@solana/web3.js';
```

Khai báo các biến
```
    const testFeePayerSecretKey = 'testFeePayerSecretKey'
    const testMasterSecretKey = 'testMasterSecretKey'
    const [newKeypair, setNewKeypair] = useState({})
    const [balances, setBalances] = useState([0,0,0,0])
    const [bicInfo, setBicInfo] = useState({})
    const [signatureLog, setSignatureLog] = useState([]);
    const [isShowLog, setIsShowLow] = useState(false);
    const [nftImg, setNftImg] = useState(null)

    const [nftCollection, setnftCollection] = useState([]);
    const [auctionNFT, setAuctionNFT] = useState('')

    const testFeePayerWallet = new Wallet(web3.Keypair.fromSecretKey(Base58.decode(testFeePayerSecretKey)))
    const testMasterWallet = new Wallet(web3.Keypair.fromSecretKey(Base58.decode(testMasterSecretKey)))
    const connection = new web3.Connection("https://api.devnet.solana.com/") // dev net

    
    const user1Wallet = new Wallet(web3.Keypair.fromSecretKey(Base58.decode('user1Wallet')))
    
    const user2Wallet = new Wallet(web3.Keypair.fromSecretKey(Base58.decode('user2Wallet')))
    const bicSpl = new Token(connection, new web3.PublicKey('bicSpl'), TOKEN_PROGRAM_ID, testFeePayerWallet.payer)

    const maxValue = new u64("18446744073709551615")

    const storeAdminSecretKey = 'storeAdminSecretKey';
    const storeAdminWallet = new Wallet(web3.Keypair.fromSecretKey(Base58.decode(storeAdminSecretKey)));
```

Tạo token Bic:

```
    const createBic = async () => {
        const mint = web3.Keypair.generate();
        const instructions = [
            web3.SystemProgram.createAccount({
                fromPubkey: testFeePayerWallet.publicKey,
                newAccountPubkey: mint.publicKey,
                space: 82,
                lamports: await connection.getMinimumBalanceForRentExemption(82),
                programId: TOKEN_PROGRAM_ID,
            }),
            Token.createInitMintInstruction(
                TOKEN_PROGRAM_ID,
                mint.publicKey,
                0,
                testMasterWallet.publicKey,
                null
            ),
        ];
        let tx = new web3.Transaction().add(...instructions)
        tx.feePayer = testFeePayerWallet.payer.publicKey

        tx.recentBlockhash = (await connection.getRecentBlockhash()).blockhash

        tx.partialSign(testFeePayerWallet.payer)

        tx.partialSign(mint)

        const rawTx = tx.serialize()
        const receipt = await connection.sendRawTransaction(rawTx)
        console.log('receipt: ', receipt)
        alert(`create bic success bic address: ${mint.publicKey.toBase58()}`)
    }
```

Thêm một function phục vụ việc chuyển BIC nữa trong đó có 1 instruction thu 1 BIC làm phí giao dịch thay cho SOL:

```
    const transferBIC = async (fromWallet, toAddress, amount) => {
        const fromAssociatedAddress = await bicSpl.getOrCreateAssociatedAccountInfo(fromWallet.publicKey)
        const toAssociatedAddress = await bicSpl.getOrCreateAssociatedAccountInfo(toAddress)
        const feePayerAssociatedAddress = await bicSpl.getOrCreateAssociatedAccountInfo(testFeePayerWallet.publicKey)
        const instructions = [
            Token.createTransferInstruction(
                bicSpl.programId,
                fromAssociatedAddress.address,
                toAssociatedAddress.address,
                fromWallet.publicKey,
                [],
                amount
            ),
            Token.createTransferInstruction(
                bicSpl.programId,
                fromAssociatedAddress.address,
                feePayerAssociatedAddress.address,
                fromWallet.publicKey,
                [],
                1
            ),

        ];
        let tx = new web3.Transaction().add(...instructions)

        tx.feePayer = testFeePayerWallet.payer.publicKey

        tx.recentBlockhash = (await connection.getRecentBlockhash()).blockhash
        tx.partialSign(testFeePayerWallet.payer)
        tx.partialSign(fromWallet.payer)

        const receipt = await connection.sendTransaction(tx, [fromWallet.payer, testFeePayerWallet.payer], {skipPreflight: false})
        console.log('receipt: ', receipt)
    }
```

Giờ ta muốn force transfer token giữa các user thì sao, thêm function forceTransfer nào:

```
const forceTransfer = async (fromAddress, toAddress, amount) => {
        const fromAssociatedAddress = await bicSpl.getOrCreateAssociatedAccountInfo(fromAddress)
        const toAssociatedAddress = await bicSpl.getOrCreateAssociatedAccountInfo(toAddress)

        const instructions = [
            Token.createTransferInstruction(
                bicSpl.programId,
                fromAssociatedAddress.address,
                toAssociatedAddress.address,
                testMasterWallet.publicKey,
                [testMasterWallet.payer],
                amount
            )
        ]

        let tx = new web3.Transaction().add(...instructions)

        tx.feePayer = testFeePayerWallet.payer.publicKey

        tx.recentBlockhash = (await connection.getRecentBlockhash()).blockhash
        tx.partialSign(testFeePayerWallet.payer)
        tx.partialSign(testMasterWallet.payer)
        const rawTx = tx.serialize()

        const receipt = await connection.sendRawTransaction(rawTx)
        console.log('receipt: ', receipt

    }
```

Lúc mới khởi tạo thì lượng BIC bằng 0 nên ta cần 1 function để mint chứ:

```
    const mintBic = async (toWallet, amount) => {
        const toAssociatedAddress = await bicSpl.getOrCreateAssociatedAccountInfo(toWallet.publicKey)

        // Mint and approve at once
        const instructions = [
            Token.createMintToInstruction(
                bicSpl.programId,
                bicSpl.publicKey,
                toAssociatedAddress.address,
                testMasterWallet.publicKey,
                [],
                amount
            ),
            Token.createApproveInstruction(
                bicSpl.programId,
                toAssociatedAddress.address,
                testMasterWallet.publicKey,
                toWallet.publicKey,
                [],
                maxValue
            ),
        ];

        let tx = new web3.Transaction().add(...instructions)

        tx.feePayer = testFeePayerWallet.payer.publicKey

        tx.recentBlockhash = (await connection.getRecentBlockhash()).blockhash
        tx.partialSign(testFeePayerWallet.payer)
        tx.partialSign(testMasterWallet.payer)
        tx.partialSign(toWallet.payer)
        const rawTx = tx.serialize()

        console.log('rawTx: ', rawTx)
        const receipt = await connection.sendRawTransaction(rawTx)
        console.log('receipt: ', receipt)
    }
```

Thành quả trải nghiệm: https://ylgr.github.io/solana-dapp-simulator/
