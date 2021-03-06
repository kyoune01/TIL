---
title: "protocol"
slug: "/reading/protocol"
date: "2002-04-00"
---

## 概要

WEB 制作の現場で使用する・目にする単語は意味がわからないものが多い。難しい専門用語のなかでも実作業からお客様への説明まで幅広い場面で使用される技術に「プロトコル（通信規約）」がある。この「プロトコル」自体の意味や普段目にすることが多いプロトコルの種類、プロトコルではないけれど関連する接続方法や仕組みについて順に説明していく。もしプロトコル自体の具体的な仕組みや他のプロトコルを知りたい場合は IT パスポート試験や基本情報技術者試験（FE）等の勉強を推奨する

## プロトコル

> コンピューター同士の通信をする際の手順や規格のこと。情報を送り出す端末の選定、データの形式、パケットの構成、エラーの対処などを取り決めた通信の約束事である。

ここまで読んでまず疑問に思うことは「プロトコルとは？」「業務で『プロトコル』って単語を聞いたことがない」だと思われる。インターネットにおけるプロトコルの仕組みは引用の通りだが、通信としての「プロトコル」はインターネットができる更に昔から存在している。例えば手旗信号は「旗を振る人間同士（コンピュータ同士）」が「ルール（規約）」に基づいて「旗を振る（パケットをやり取りする）」プロトコルである。このように広義では通信をおこなううえで定めたルール全般をプロトコルといい、IT ではコンピュータ同士のやり取りをする規約のことをプロトコルと呼んでいる

ただし業務や日常会話で『プロトコル』の単語自体を発言することはほとんど無い。しかし誰もが無意識に使用しているプロトコルが 1 つ存在する。「http」である。何気なくブラウザへ打ち込んでいるが、そもそも http とは何なのか？

## http

> HTTP は、 「Hyper Text Transfer Protocol」の略です。 今やインターネットの代名詞となった WWW(World Wide Web)上で Web サーバとクライアントが、 HTML(Hyper Text Markup Language = Web ページを記述するための言語)で書かれた文書などの情報をやりとりする時に使われる通信手順(プロトコル)を意味します。

http とは主にブラウザで WEB ページを表示するときに使用するプロトコル。簡単にいうと「テキストファイルを受け取るための仕組み」である。引用文で「WEB ブラウザ」だけを指定せず「クライアント」と記載しているのは、あくまで http は「通信規約」であり使う用途を指定しないため。例えば WEB スクレイピングなどプログラムからアクセスしたり wget/curl でダウンロードしたり、インターネット経由でファイルをダウンロードする際にも使用できる。http は WEB 以外でも使用できることを覚えておくとよい

http に並んで打ち込む https という単語もあるが、実は http≠https ではなく http≒https であり、http と異なるプロトコルではない。https の説明をするために「SSL/TLS」を説明する

## SSL/TLS(https)

http には暗号化の仕組みがない。安全に通信するために通信内容を保護できる SSL（Secure Sockets Layer）が開発された。SSL を用いることで通信の「暗号化」「正当性の確認」「認証」を実現していた。しかしコンピュータのスペック向上や解読アルゴリズムの発見により SSL の暗号が解読されたため、次の暗号化の仕組みとして TLS（Transport Layer Security）が開発された。SSL や TLS によって保護された http を https と呼ぶ

※普段意識することがないため混同しがちだが狭義では SSL≠TLS のため、伝える相手によって表現を変える必要がある

```
http + SSL/TLS
     ↓
   https
```

ここからは WEB サービスを運用するうえで必要になるプロトコルを各自紹介する

## SMTP/POP

WEB サービスのなかではフォーム入力を完了した通知をメールで送信するサービスが存在する。「受信」するだけで良い http と違いメールは「送信」「受信」の 2 つの動作が必要である。そのためメールを送信する SMTP（Simple Mail Transfer Protocol）と受信してクライアント本体に保存する POP（Post Office Protocol）の 2 つの規約によって「メール」は構成されている。しかし近年情報端末が PC だけでなくスマートフォンなど複数の媒体が増えてきたことで「どの端末でも同じメールを確認したい」ことがある。そのため POP に代わって IMAP（Internet Message Access Protocol）という受信データをサーバに保存する規約も存在する

## FTP

FTP（File Transfer Protocol）はファイルを送受信する規約。FFFTP や FileZilla など、FTP で接続するソフトもまとめて FTP と呼ぶことがある。http と FTP の違いは「クライアントがファイルを送信できる（FTP：双方向）か、受信専用（http：一方向）か」。以前はファイルを本番サーバに公開するための接続方法として主流だったが FTP はセキュリティに問題があるため、近年では SSH での接続を推奨しており FTP は使用すべきではない

## SSH

> SSH とは、Secure Shell（セキュアシェル）の略称で、リモートコンピュータと通信するためのプロトコルです。認証部分を含めネットワーク上の通信がすべて暗号化されるため、安全に通信することができます。

近年オンプレからクラウドや VPS などが主流になり、手元にサーバがある時代ではなくなった。遠隔地にあるサーバへファイルを送信する方法として以前までは上記の FTP がサーバ接続の方法として主流であったがセキュリティに問題がある。セキュリティの問題を解決するために、公開鍵暗号を利用して通信内容を保護できる仕組みとして SSH が開発された

## VPN

> VPN 接続とは、インターネット上に仮想の専用線を設定し、特定の人のみが利用できる専用ネットワークです。接続したい拠点（支社）に専用のルーターを設置し、相互通信をおこなうことができます。

自社サーバに置かれた機密情報へ外部ネットワークからアクセスする場合、社外の人間からはアクセスさせず社内の人間だけを許可したい。どうやって特定の人間だけをセキュアに接続できるか、その解決策として専用線の代わりに VPN（Virtual Private Network）が開発された。VPN によって専用線が持つ「特定の人間のみのアクセスを許可する」メリットをインターネットがつながる場所ならどこでも享受できる。

しかし VPN は「特定の人であれば安全」という考えのもとに成り立っており、アクセスしてくる環境やウイルスに対しては社内ネットワークを保護できていない。PC が乗っ取られたり通信傍受をされたり、今の時代において VPN はセキュアな接続であると言えなくなっている。Google など世界の企業では、VPN を廃止した次のネットワークとして「ゼロトラスト・ネットワーク」という考え方を基本に、 VPN を廃止したネットワークを構築している。

## API

> 「API」とは、「Application Programming Interface」の頭文字です。～大雑把に言うと「アプリケーションをプログラミングするためのインターフェース」という意味です。

> API とは、この「何か」と「何か」が「アプリケーション、ソフトウェア」と「プラグラム」をつなぐもの、という意味になります。

近年サービスをつくるときに全てを 0 から実装することは少なくなっている。ではどうやってサービスを提供するかというと、サービスに必要な機能を分割する。例えばサービスの中で今日の天気を知る必要があれば [天気予報 WEBAPI](https://qiita.com/cnakano/items/ff3fd90f685f4ca363cc) を利用する。もし API を利用しない場合、世界中の気象レーダーのデータを取得する契約をするか自社で気象レーダーを建てる必要があり、莫大なコストが発生する。API を利用することで開発者は利用したいデータの処理方法は知らず、あくまでサービスとして提供したい機能の開発に注力できる。この仕組みを API と呼ぶ

現在 WEBAPI のレスポンスは JSON 形式が主になっており、実装例としては「RESTfull API」や「GraphQL」が主流である。上記では一般公開されている API を例として挙げたが、大規模開発では API を自社開発することもある。また WEB に公開されている（http で叩ける）API を WEBAPI と呼ぶが API 自体の接続方法は WEB に限らない。言語・パッケージとは異なるサーバ内の別アプリケーションと連携することも API の分類なので、WEBAPI だけを API と認識すると齟齬が生まれるので注意が必要

## あとがき

WEB 開発に携わる上で上流のプロトコルだけでなく通信方法などの知識も必要になる。新卒時には VPN が概念すら理解できておらずマジで怒られた。その時に後悔して初めて勉強したことで、ここで紹介していないものも含めて WEB・サーバ・業務を支えている仕組みが沢山存在することを知った。マークアップ業務だけでなくお客様とのやり取りや高度なサービスの設計に携わっていきたいならば「そもそも会話ができない」状況に陥らないように、目の前の見慣れない単語から少しづつ調べておくことが大事だと思う（マジで怒られる前に）

## 参考

- [プロトコル](https://www.otsuka-shokai.co.jp/words/protocol.html)
- [HTTP とは](https://www.nic.ad.jp/ja/basics/terms/http.html)
- [HTTPS と SSL と TLS：その違いを５分でわかりやすく解説！](https://blog.qbist.co.jp/?p=1441)
- [メール設定で最初につまずく『SMTP』『POP』『IMAP』 その意味＆設定方法は？](https://time-space.kddi.com/ict-keywords/kaisetsu/20170824/2081)
- [メール設定の“POP”と“IMAP”、いったいなにが違うの？](https://cs.myjcom.jp/jplus/articleDetail?cn=20171026155110)
- [ダウンロード時の「HTTP」と「FTP」の違い](http://happyking.blog47.fc2.com/blog-entry-58.html)
- [用語集｜ SSH](https://www.idcf.jp/words/ssh.html)
- [VPN 接続とは？VPN の基本とメリット・デメリットを紹介](https://www.nttpc.co.jp/column/network/whats_vpn.html)
- [米グーグルはテレワークで VPN を使わない、なぜなら「あれ」が危険だから](https://xtech.nikkei.com/atcl/nxt/column/18/00692/031000023/)
- [今さら聞けない IT 用語：やたらと耳にするけど「API」って何？](https://data.wingarc.com/what-is-api-16084)
