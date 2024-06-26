---
title: "textEncode"
slug: "/reading/textEncode"
date: "2002-05-00"
---

## 概要

近年文字化けを見る機会はかなり少なくなったが、昔のファイルを運用する際に文字化けと出会うことがある。文字化けが起きる原因は文字コードの誤変換と言われているが、そもそも文字コードとは何なのか

文字コードは 1 冊の本として出版されるほど歴史がある・種類が多いため、詳しく説明するためには学術側へ踏み込む必要がある。本資料ではあくまで「文字コードを利用する」ための記述に留まり詳しい記述はしない。もし詳しく知りたい場合は下記を参考にする・資格取得を目指すと良い

参考資料：[[改訂新版]プログラマのための文字コード技術入門](https://www.amazon.co.jp/dp/4297102919/ref=cm_sw_r_tw_dp_x_H1-jFbH8HNP71)

## 文字コードとは

動作を 0 と 1 で構成しているコンピュータは文字どころか仕組みがなければ数字すら認識できない。コンピュータが文字を認識するとき「文字列と表現したい文字の対応表」を見ながら「文字を数字で表現できる仕組み」に表現したい文字列を渡すことで文字を入出力している。「文字コード」と呼ばれる仕組みは下記 2 つの仕組みを総称して呼ばれている

1. 文字集合（文字と数字の対応表）
1. エンコーディングスキーム（文字の符号化、文字を数字で表現できる仕組み）

文字コードと言われて想像する用語に ASCII、Shift_JIS、Unicode、UTF-8 がある。対応表と仕組みのそれぞれを指している用語ではあるがどちらも「文字コード」で伝わるため、使い分けに必要な学習コストを考えると特別な意図が無い限り、使い分ける必要はない

### 文字集合（文字と数字の対応表）

文字集合には主に「Unicode」や「JIS 文字コード」「Shift_JIS」などがあたる

日本語を表示するため初期に開発された「JIS 文字コード」は windows でも使用されている（されていた）文字コード。対して日本語だけでなく世界の文字を共通の文字コードで表現するため後発の「Unicode」が日々様々なツール・言語で標準化されている

### エンコーディングスキーム（文字の符号化、文字を数字で表現できる仕組み）

Unicode や Shift_JIS を使用して表示する仕組みとして「UTF-8」や「ISO-2022-JP」「シフト符号化表現」が存在する

符号化方式は最初期に「ASCII」が存在したが、1 バイトでは日本語などアルファベット以外の文字を表現できなかった。ASCII で表現できない日本語を表現するために様々な規格・符号化方式が開発された。なぜ初めから Unicode が生まれなかったのかは、「ISO」や「国際規格」が生まれた理由を参考にするとよい

### 日本でよく見る文字コード

| 文字集合                | 符号化方式       |
| ----------------------- | ---------------- |
| Unicode                 | UTF-8            |
| Unicode                 | UTF-16           |
| Unicode                 | UTF-32           |
| ISO/IEC 2022            | ISO-2022-JP      |
| Extended Unix Code(EUC) | EUC-JP           |
| Shift_JIS               | シフト符号化表現 |

## 文字化けの原因

これだけ文字コードが存在していると「どの文字コードで表現するか判断できない」ことが想定される。この不具合が起きたため無理やり表現されたテキストを「文字化け」と呼ぶ

解決方法は簡単で正しい文字コードで表示するよう設定を切り替えるのみである。もし意図した文字コードを選択しているにも関わらず文字化けが治らない場合、無理やり表現したテキストで上書き保存している可能性がある。この場合はテキストを戻す手段がないので諦めること

## どの文字コードを使うべきか？

結論から記載すると「Unicode を使用するべき」である。どの文字コードを選んでも正しい文字コードを選ばなければどの環境でも文字化けは発生する。文字化けを防ぐには「ファイル・システム内で使用している文字コードを予め指示する」と共に「広く使われている文字コードを使用する」ことが重要である

世界で共通の文字コードを使用するべく開発されている Unicode は Windows や Mac の OS だけでなく、Python など言語内部でも採用されており選択しない理由がない。また絵文字が策定されているのは Unicode であり、サービス提供としても Unicode 対応は必須である

ちなみに、通例として WEB アプリ開発で Shift_JIS/ISO-2022-JP を選択することがある。しかし 2020 年現在、両者を選択する必要はほぼ存在しない。「古い環境を担保する」ことを採用する理由として挙げられるが JIS 文字コード にしか対応していない環境は他の脆弱性が存在する可能性が高いため、リスクヘッジとしてそもそも担保しない方がよい

## 文字コード Tips

Unicode の採用を推奨したが、Unicode が対応していない状況は多々存在する。対応していない状況も含めた文字コードに関する Tips を紹介する

- Windows のメモ帳は ANSI (Shift_JIS)をデフォルト採用していた。ただし windows10 バージョン 1903 から UTF-8 に変更された
- エクセルは初期設定で Shift_JIS を使用する。もし CSV ファイルを UTF-8 で作成した場合「エクセルで開くと文字化けするんですが…」という"バグ報告"を受けるかも
- Unicode には「BOM 付き」が存在する。WEB 開発で BOM は必要ないが、アプリが自動で付与することがある。もし Unicode で文字化けが治らない場合は BOM 付きに注意
- cmd の標準出力は cp932。Shift_JIS として一応扱えるが微妙に違う。プログラムで標準出力から値を取得するとき、日本語は取得できないものとして諦めること

## あとがき

わざわざ 2020 年にもなって文字コードを意識しながら WEB 開発をしたくないと思うときがある。ただしそれは「意識したくない」であって「知らなくて良い」ではない。文字コードを知らなければ直接文字を記載された、いつ文字化けするか分からない正規表現を量産することになるし、DB のカラムに設定された文字コードが異なることを知らずにバグ探しをすることになる。でもやっぱり文字コードは意識したくないので全部 UTF-8 になってほしい… いや絵文字対応が完了してからでもいいかな……

## 参考

- [知っておきたい！ 文字コードの基礎知識 ……ASCII，シフト JIS，Unicode etc.](https://gihyo.jp/book/pickup/2019/0006)
- [文字コード入門](http://www.shuiren.org/chuden/teach/code/index-j.html)
- [文字コード - Wikipedia](https://ja.wikipedia.org/wiki/%E6%96%87%E5%AD%97%E3%82%B3%E3%83%BC%E3%83%89)
- [UTF-8 の BOM 付き・BOM 無しの違いと確認方法](https://uxmilk.jp/48923)
