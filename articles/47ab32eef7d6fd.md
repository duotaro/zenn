---
title: "Remixを使ってスマートコントラクト(solidity)をSepoliaにデプロイする"
emoji: "⛓️"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["Remix", "スマートコントラクト", "デプロイ", "Sepolia", "Solidity"]
published: true
---

# Remixを使ってスマートコントラクトをSepoliaにデプロイする
今回は[Remix](https://remix.ethereum.org/)を使って、スマコンをSepoliaにデプロイする方法を紹介します。
後述しますが、他のチェーンへのデプロイも簡単にできるはずです。（やってない）


## スマートコントラクト実装
File exploerメニューを開きます。
contractフォルダがあるのでsolidityファイルを作成して、スマコンを実装してください。
![](https://storage.googleapis.com/zenn-user-upload/d397ddaab079-20240529.png)


## コンパイル
デプロイしたいファイルを開いた状態で、Solidity Compilerメニューを開きます。
![](https://storage.googleapis.com/zenn-user-upload/2bad8532a8ad-20240529.png)

「Compile 対象ファイル」というボタンが出ているはずなので押します。
成功すれば画像のようになります↓
![](https://storage.googleapis.com/zenn-user-upload/b9b4e45a4d24-20240529.png)

ABIファイルなどを使う場合は、ここでコピーできます。

## デプロイ
メタマスクなどweb3用のウォレットを持っていない方はインストールしてから進めてください。
:::message alert
ウォレットの準備が必要
:::
Deploy & run transactionsメニューに移動します。コンパイルが成功していれば、CONTRACTの項目に先ほどのファイル名が表示されているはずです。
![](https://storage.googleapis.com/zenn-user-upload/d6c0ef2390e9-20240529.png)

次に一番上のENVIRONMENTの項目で「Injected Provider」を選択します。
私はRabbyウォレットを愛用しているので「Injected Provider - Rabby Wallet」と表示されていますが、ここは人によって変わってくるはずです。
![](https://storage.googleapis.com/zenn-user-upload/216dc075124a-20240529.png)

「Injected Provider」を選択するとウォレット接続できます。
接続したウォレットの接続チェーンをSepoliaにしましょう。
ここで選択したチェーンがデプロイ対象となるはずなので、もしETHメインネットにデプロイしたい場合はETHメインネットに接続します。
逆に言えば接続するチェーンを間違ってしまうと、デプロイ先が変わってしまい、そのチェーンでの手数料が取られますので注意してください。
:::message 
ウォレットの接続先でデプロイ先が変わるので注意
:::
接続できたらACCOUNTの項目に接続したウォレットのアドレスが表示されるので確認しましょう。
また、接続先チェーンのchainIDがENVIRONMENTの項目の下に表示されているはずなので、そちらも確認してください。

確認できたらデプロイするだけですが、デプロイには手数料がかかります。
SepoliaにデプロイするにはSepoliaETHが必要です。
[alchemy faucet](https://www.alchemy.com/faucets/ethereum-sepolia)からもらえます。
最近はbot対策で、メインネットのETHの量やgitcoin passportのポイントでfauceの制限を行っていることがあります。
:::message alert
faucetが使えない場合もある
:::

fauceでSepoliaETHをゲットしたらデプロイを押します。
デプロイのトランザクションIDがログなどに出力されるので、exploerで確認しましょう。
正しくデプロイできていればコントラクトアドレスも画面下の方に表示されるはずです。

### 参考
https://eng.shibuya24.info/entry/connect_remix_to_metamask
https://smacon.dev/posts/remix-tutorial/

### おわり
