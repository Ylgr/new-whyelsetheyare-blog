---
layout: blog
title: "Khai mở, thế giới NFT - Phần 2: Solana NFT - Chương 1: Thuộc tính cho
  những token"
date: 2022-04-22T10:54:04.892Z
top_image: /images/uploads/26309160_p0.jpg
tags:
  - nft
  - program
  - code
  - solana
  - metaplex
categories:
  - Lập trình
  - NFT
---
Câu chuyện sẽ đơn giản nếu NFT chỉ mang tính chất giá trị. Tại sứ sở có nhịp sống hối hả như Solana, thứ mà người ta đề cao ở NFT đó là tính trải nghiệm.

Bạn vừa vẽ ra một con rồng tuyệt vời và biến nó thành NFT, giờ thì bạn muốn hiện thực hóa sức mạnh của nó, đem nó đi thiêu rụi cả thành phố và tổn hao máu nếu có hiệp sĩ chiến đấu với nó. Ồ,ở đây chúng ta có một vài sự thay đổi thuộc tính và cần tốc độ xử lý nhanh và rẻ để tăng trải nghiệm. Thế giới NFT tại Solana là lựa chọn tối ưu cho việc này

<!-- more -->

# 1. Ở đây có NFT!

Nếu bạn đã xem qua bài viết trước của tôi nói về chuẩn SPL token trên hệ sinh thái Solana thì như chúng ta đã biết, bên Solana chỉ có một chuẩn duy nhất dùng cho cả fungible token, semi-fungible token và non-fungible token.

Ủa, thế thì việc sinh ra NFT đơn giản quá còn gì, ta chỉ cần sinh ra một token mới với số lượng có hạn, sau đó bỏ quyền mint đi là được, đúng không? 

Chính xác là thế, có điều bị thiếu, NFT ngoài tính duy nhất nó còn có data. Cho nên với cách làm trên, thứ bị thiếu sẽ là yếu tố về dữ liệu. Câu hỏi là làm thế nào để bỏ một đoạn uri vào một spl token - thứ mà vốn dĩ không được thiết kế để chứa thông tin này?

Từ khóa để trả lời câu hỏi trên là Metaplex.

# 2. Chào mừng bạn đến với thế giới Metaplex

![](https://global-uploads.webflow.com/606076d78f6b1c80e91a9a0a/60be476fbf4e026877255812_SOLANA%20NEWS%20Introducing%20Metaplex_%20NFT%20Minting%20on%20Solana.jpg)

Metaplex, nói ngắn gọn là một hệ sinh thái nhiều thành phần để hỗ trợ việc xử lý và các hoạt động liên quan tới NFT. Hơn cả Opensea ở các nền tảng EVM, do tính chất PDA của program nên việc sử dụng Metaplex đơn giản hơn bao giờ hết đó là bạn chỉ cần gọi program của Metaplex để tạo PDA cho riêng bạn sử dụng là được, và Metaplex rất hoan nghênh việc này. Yay!

Thế giới của Metaplex cũng rất chi là complex về mặt kỹ thuật và phát triển, còn về mặt ứng dụng nôn na Metaplex có những thứ sau:

* Token metadata: Đây chính là mảnh ghép còn thiếu của một token spl. Nôm na là sau khi tạo một spl token mà bạn sử dụng với mục đích NFT, bạn cần thêm một bước là làm việc với program này để đẩy dữ liệu uri lên.
* Auction house: Cái tên nói lên tất cả, đây là sàn đấu giá chuyên nghiệp tầm cỡ Solana cho các NFT, opion tại đây mở hơn so với Opensea và hệ thống master edition rất là sang chảnh, nó hoạt động như một hình thức phân phối bản quyền mà điều này khiến tôi nghĩ có khi Steam sẽ lên đời NFT dùng thứ này.
* Candy machine: Nhà máy kẹo, đúng ở nghĩa nhà máy hoặc đúng cả ở kẹo trong một vài use case. Là một hệ thống in và phân phối NFT được implement các cơ chế chống gian lận để đảm bảo công bằng, thực hư chuyện này ra sao thì hãy cùng tìm hiểu sau nhá (hiện tại tôi cũng chả biết nó làm sao nữa).
* Phần còn lại mà sẽ không đề cập chi tiết: Fair launch - giao thức để người mua đấu giá NFT trong 1 khoảng giá mà các nghệ sĩ mong muốn, Gumdrop - hỗ trợ airdrop nhiều user trong 1 danh sách whitelist ở giá rẻ cho chủ sở hữu NFT, Fireball, Fusion, ...

# 3. Chặng đầu metaplex - Token metadata

Metadata, nôn na nó là cái data chứa trong file json đặt ở uri của các NFT dạng dạng thế này:

![](https://miro.medium.com/max/1400/1*8no0xmIMH4ZxN5A_CehE0A.png)

Những dữ liệu này được fix cứng nên đảm bảo tính bất biến của sản phẩm khi cung cấp dịch vụ.

Giờ chúng ta thực hành với chúng nào.

Việc đơn giản nhất để tương tác với metaplex với phần đa dev là dùng Js, tại đây chúng ta có sẵn lib rồi, mặc dù chưa đầy đủ tính năng cho lắm vì đang trong quá trình phát triển: https://github.com/metaplex-foundation/js

Nên ta cần sử dụng thêm lib đã ổn định để đi kèm: https://www.npmjs.com/package/@metaplex-foundation/mpl-token-metadata

Ok chuẩn bị vậy là ổn rồi, let's code:
 
Đầu tiên ta cần setup connection và wallet:

```
import {web3, Wallet, BN} from '@project-serum/anchor';


    const connection = new web3.Connection("https://api.devnet.solana.com/") // dev net;

    const wallet = new Wallet(web3.Keypair.fromSecretKey(""));
```

Chuẩn bị một function để còn tạo SPL token vì bản chất NFT trên Metaplex cũng là SPL token mà:

```
    async function prepareTokenAccountAndMintTxs(
        connection,
        owner,
    ) {
        const mint = web3.Keypair.generate();
        const mintRent = await connection.getMinimumBalanceForRentExemption(82);
        const createMintTx = new programs.CreateMint(
            { feePayer: testFeePayerWallet.publicKey },
            {
                newAccountPubkey: mint.publicKey,
                lamports: mintRent,
                owner: owner,
                freezeAuthority: owner
            },
        );

        const recipient = await Token.getAssociatedTokenAddress(
            ASSOCIATED_TOKEN_PROGRAM_ID,
            TOKEN_PROGRAM_ID,
            mint.publicKey,
            owner,
        );

        const createAssociatedTokenAccountTx = new programs.CreateAssociatedTokenAccount(
            { feePayer: testFeePayerWallet.publicKey },
            {
                associatedTokenAddress: recipient,
                splTokenMintAddress: mint.publicKey,
                walletAddress: owner
            },
        );

        const mintToTx = new programs.MintTo(
            { feePayer: testFeePayerWallet.publicKey },
            {
                mint: mint.publicKey,
                dest: recipient,
                amount: 1,
                authority: owner
            },
        );

        return { mint, createMintTx, createAssociatedTokenAccountTx, mintToTx, recipient };
    }
```

Và cuối cùng là một vài thông tin NFT ta setup:
```
        const uri = "https://aecwobcvprkxm2kgewrjduk5jd5uqzywxcmru6z6wms2tifhxwkq.arweave.net/AQVnBFV8VXZpRiWikdFdSPtIZxa4mRp7PrMlqaCnvZU/"
        const maxSupply = 5
```

Giờ thì bắt đầu Metaplex nào! Khởi động bằng việc tạo spl token và setup các element:

```
import {
    Metadata,
    MetadataKey,
    MasterEdition,
    Creator,
    MetadataDataData,
    CreateMetadata, CreateMasterEdition,

} from '@metaplex-foundation/mpl-token-metadata';
import { utils, programs } from '@metaplex/js';


        const { mint, createMintTx, createAssociatedTokenAccountTx, mintToTx } =
            await prepareTokenAccountAndMintTxs(connection, wallet.publicKey);

        const metadataPDA = await Metadata.getPDA(mint.publicKey);
        const editionPDA = await MasterEdition.getPDA(mint.publicKey);

        const {
            name,
            symbol,
            seller_fee_basis_points,
            properties: { creators },
        } = await utils.metadata.lookup(uri);
```

Giờ thì khởi tạo metadata và đẩy nó lên Blockchain nào:

```
        const creatorsData = creators.reduce((memo, { address, share }) => {
            const verified = address === wallet.publicKey.toString();

            const creator = new Creator({
                address,
                share,
                verified,
            });

            memo = [...memo, creator];

            return memo;
        }, []);

        const metadataData = new MetadataDataData({
            name,
            symbol,
            uri,
            sellerFeeBasisPoints: seller_fee_basis_points,
            creators: creatorsData,
        });

        const createMetadataTx = new CreateMetadata(
            {
                feePayer: testFeePayerWallet.publicKey,
            },
            {
                metadata: metadataPDA,
                metadataData,
                updateAuthority: wallet.publicKey,
                mint: mint.publicKey,
                mintAuthority: wallet.publicKey,
            },
        );

```

Cuối cùng là tạo một master edition cho NFT đó để phục vụ việc buôn bán sau này:

```
        const masterEditionTx = new CreateMasterEdition(
            { feePayer: testFeePayerWallet.publicKey },
            {
                edition: editionPDA,
                metadata: metadataPDA,
                updateAuthority: wallet.publicKey,
                mint: mint.publicKey,
                mintAuthority: wallet.publicKey,
                maxSupply: maxSupply ? new BN(maxSupply) : null,
            },
        );
```

Cuối cùng combine data lại thành các instruction và đẩy lên Solana network nào:

        const finalTx = fromCombined([
            createMintTx,
            createMetadataTx,
            createAssociatedTokenAccountTx,
            mintToTx,
            masterEditionTx,
        ], { feePayer: testFeePayerWallet.publicKey })
        finalTx.recentBlockhash = (await connection.getRecentBlockhash()).blockhash;

        finalTx.partialSign(mint)
        finalTx.partialSign(testFeePayerWallet.payer)
        finalTx.partialSign(wallet.payer)
        const txId = await connection.sendRawTransaction(finalTx.serialize())
        console.log('txId: ', txId)

```

Nếu các bạn notify thì đoạn code trên chỉ định một người khác làm fee payer đó.
Giờ coi log tx và enjoy NFT mới tạo nào.

Hẹn bạn ở hành hành trình đấu giá phía trước.