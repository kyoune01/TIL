---
title: "principles"
slug: "/reading/principles"
date: "2002-03-00"
---

## 概要

オブジェクト指向によってプログラミングが発展していく中で「こう書くべき」とも言われる「原則」というコード作法が確立されていった。WEB 開発において関わりがないように思えるオブジェクト指向だが、WEB 技術もプログラミングの歴史から発展している。原則を知ることで、WEB に関わらず、プログラミングの土台を広げる

本資料の目的は「原則を自分の言葉で説明する・できるようになる」である。そのため、オブジェクト指向のコード作法を WEB 技術に置き換えたことで意味が通らない・曲解した表現になっていることがある。もし本資料より良い例・表現がある場合は指摘を

説明する原理は下記の通り

- KISS
- DRY
- YAGNI
- SOLID
- デメテルの法則
- 関心の分離
- 単一責任の原則
- オープン・クローズドの原則
- SOLID ※含まれている原則の紹介のみ

### 参考

- [10 Basic Programming Principles Every Programmer Must Follow](https://www.makeuseof.com/tag/basic-programming-principles/)
- [何かのときにすっと出したい、プログラミングに関する法則・原則一覧](https://qiita.com/hirokidaichi/items/d6c473d8011bd9330e63)

## KISS

Keep it simple stupid.（シンプルで愚鈍にする）

### なぜ必要か

例えばクライアント指示で LP に JS で動きを入れた結果ローディング待機時間が延びユーザーの離脱につながったという事例。要件は要件としても、シンプルに作っておけば更に利益を得られたという場面が往々にして存在する。コードも同じように短ければ短いほど良い。長いコードは読むと疲れる

### どう使うか

共通して大事なことは「できるだけシンプルに、無駄な記述をしない」

- HTML をマークアップ中「ここはレイアウトが難しいから全部同じ section に入れてしまおう」はしない。要素を意味単位できちんと分割する
- 「コーディング中にファイルによってインデントが変わってしまったがルールがないのでそのままにした」はしない。誰がどのファイルを触っても同じルールでコーディングできるようにする
- 初回制作から何度も修正が発生して巨大になった処理の行数を数行だけでも短くする

### 参考

- [阿部寛さんから学ぶ KISS(Keep it simple, stupid)の原則](https://qiita.com/DeployCat/items/09bb6831b029f5185b33)

## DRY

Don’t Repeat Your Self（繰り返しを避けること）

### なぜ必要か

前提の考えとして「重複は無駄である」。テキストの差し替え指示がきたときに重複している箇所が存在すると、重複箇所と同じ回数同じ作業が発生する。また重複箇所に気づけなかった場合は重大な事故にもつながる

またコーディングだけでなく日々の業務にも繰り返していることがないか日々意識する

### どう使うか

重複は無駄であるが新規のコードより現在動いているコードを信用する考え方も同時に存在する。そのため「3 回目のコピーが必要になったときは共通化する」を指標とすることが多い

- 毎日手動でアクセスデータを取得してエクセルに入力している。無駄なので自動化対象
- 個別 CSS を当てている見た目の似たボタンが複数存在する。コンポーネントに落とし差異を modifer として管理する
- 同じ動きをする JS の処理をコピーし、クラス名のみ変更しようとした。処理を関数にしイベントハンドラで呼び出すように修正する

### 参考

- [DRY 原則](https://xn--97-273ae6a4irb6e2hsoiozc2g4b8082p.com/%E3%82%A8%E3%83%83%E3%82%BB%E3%82%A4/DRY%E5%8E%9F%E5%89%87/)

## YAGNI

You Ain’t Gonna Need It（余計な機能を付けるな！）

### なぜ必要か

仕事では事前に予測して準備しておくことが優れた能力だと言われるがコーディングにおいては真逆である。例えばクライアントへ提案するデザインを準備する場合、SPA で組んでも HTML で組んでも Photoshop で組んでも、パワーポイントで提案するだけならまったく関係がない

機能は実際に必要となるまでは追加しない

### どう使うか

コーディングは要件を過不足なく達成することを意識する

- CSS をコーディング中「 .marginTop-10px を用意しておけば後々使うかも」はしない。汎用クラスはルールにない限り必要になるまで不要
- JS で関数をコーディング中「この変数は別で使いそうだからグローバルに置こう」はしない。本当にしないで

### 参考

- [YAGNI 原則とは |「分かりそう」で「分からない」でも「分かった」気になれる IT 用語辞典](https://wa3.i-3-i.info/word17076.html)

## デメテルの法則

直接の友達とだけ話すこと。自分以外の構造などに対して持っている仮定を最小限にする

### なぜ必要か

例えばコードの中である変数に依存している（ウィンドウサイズなどブラウザ JS が持つデータ・Ajax で取得した JSON データ）処理があるとする。もし依存したデータの構造が変更された場合、コードの更新が必要になるがその修正箇所を短く・限定できれば工数を短くできる。その状態・コードはデメテルの法則を守っていると言える

### どう使うか

jQuery を使用しているとまれに下記のような指定方法を見ることがある。しかし下記では「main クラスがない」「main クラス内に nav_list がない」「nav_list が 1 つしかない」など小さな理由で動作しなくなる

```javascript
const $element = $(".main").find(".nav_list_item:nth-child(2)")
```

上記を ID 指定に書き換えるだけでシンプルに・依存せずに取得ができる。普段からよく見る「js-〇〇」の書き方は直感で分かりやすくするだけでなく、依存をなくす書き方をすることもできる

```javascript
const $element = $("#js-target")
```

### 参考

- [デメテルの法則を厳密に守るにはどうすればいいの？](https://qiita.com/br_branch/items/37cf71dd5865cae21401)

## 関心の分離

プログラムを関心（何をしたいのか）毎に分離された構成要素で構築する

### なぜ必要か

例えば下記のようなフォルダ構成の WEB サイトが存在していると「共通 css と個別 css」の違いが分からないためミスが起きやすくなる。このように異なる役割のファイル・処理は分離することで不要なミスをなくすことができる

```tree
/html
  ├ /css
  │ ├ style.css
  │ └ component.css
  ├ /sub
  │ └ index.html
  └ index.html
```

### どう使うか

コードでは「1 つの動作の中でいくつの機能が存在するか」を見つけて切り分けることで関心を分離できる。

```javascript
// 役割1．対象選択
// 役割2．発火イベント設定
$("#js-localnav_btn").click(
  // 役割3．処理
  function () {
    if ($(".localnav").hasclass("is-localnav")) {
      // 役割4．処理A
      $(".localnav").addClass("is-localnav")
    } else {
      // 役割5．処理B
      $(".localnav").removeClass("is-localnav")
    }
  }
)
```

上記の例はコード量が短いため恩恵を感じないかもしれないが「他のイベントでもクラスの制御をしたい」等の修正が発生する未来の運用を考えると修正後のコードが優れている。また「.localnav」など要素の記述がそれぞれ 1 度で済むため修正しやすい

```javascript
// 役割3．処理
function toggleLocalnav(classname) {
  $localnav = $(".localnav")
  if ($localnav.hasclass(classname)) {
    hiddenLocalnav($localnav, classname)
  } else {
    showLocalnav($localnav, classname)
  }
}
// 役割4．処理A
function showLocalnav($element, classname) {
  $element.addClass(classname)
}
// 役割5．処理B
function hiddenLocalnav($element, classname) {
  $element.removeClass(classname)
}

// 役割1．対象選択
$btn = $("#js-localnav_btn")
// 役割2．発火イベント設定
$btn.on("click", toggleLocalnav(".is-localnav"))
```

## 単一責任の原則

クラスを変更する理由が 2 つ以上存在してはならない

### なぜ必要か

元々はオブジェクト指向で書かれたコードに対しての設計手法。もし複数の機能が必要なクラスが存在した場合、それぞれに対して仕様変更が発生すると複数回コード変更を受ける。歴史が経つにつれスパゲッティコードになりやすい

関心の分離でも暗黙的に触れたが「1 つの動作・要素＝ 1 つの役割・仕事」を守ることが重要。1 処理で複数のことを同時進行したり、1 人が複数の責任をもつ状態は避けるべきである。ビジネスではマルチタスクという言葉もあるが、実際のプログラムではシングルスレッド／シングルプロセスに最適化して処理している。

### どう使うか

コード例は関心の分離を参考

### 参考

- [オブジェクト指向設計原則とは](https://qiita.com/UWControl/items/98671f53120ae47ff93a)

## オープン・クローズドの原則

拡張に対して開いていて、修正に対して閉じていなければならない

### なぜ必要か

「動いている既存コードは正である」という考え方からすると、拡張（既存の動作を変えずに追加のみ）する場合はできるだけ既存コードを触りたくない。逆に既存のコードを修正する場合はできるだけ周りの動作に影響を与えたくない。「開く＝追加だけで済む」「閉じる＝周りに影響を与えない」コードが良いコードである

### どう使うか

コーディング時に追加・修正する場合はどう手を加えるかを意識してコーディングする。例えば CSS で下記のような記述がある場合

```css
.list_item_red {
  box-sizing: border-box;
  color: #ff1111;
  width: 100px;
}
.list_item_blue {
  box-sizing: border-box;
  color: #0000ff;
  width: 100px;
  border: 1px solid #ccccff;
}
```

このままでは追加も拡張も難しいため下記のように書き換える。すると異なる体裁を追加するときに重複する記述をコピペしなくてもよいし、修正する場合は最低限の修正で済む

```css
.list_item {
  box-sizing: border-box;
  width: 100px;
}
.list_item-danger {
  color: #ff1111;
}
.list_item-clear {
  color: #0000ff;
  border: 1px solid #ccccff;
}
```

### 参考

- [オブジェクト指向設計の原則](https://thinkit.co.jp/article/13274#:~:text=%E3%82%AA%E3%83%BC%E3%83%97%E3%83%B3%E3%83%BB%E3%82%AF%E3%83%AD%E3%83%BC%E3%82%BA%E3%83%89%E3%81%AE%E5%8E%9F%E5%89%87%E3%81%A8,%E3%81%99%E3%82%8B%E3%81%B9%E3%81%8D%E3%80%8D%E3%81%A8%E3%81%84%E3%81%86%E6%8C%87%E9%87%9D%E3%81%A7%E3%81%99%E3%80%82)

## SOLID

これまで説明してきた原則もあわせた 5 つの原則をあわせて SOLID と呼ぶ

- S：SRP、単一責任の原則
- O：OCP、オープン・クローズドの原則
- L：LSP、リスコフの置換原則
- I：ISP、インタフェース分離の原則
- D：DIP、依存性逆転の原則

## あとがき

ここまで原則を説明してきたが、正直説明されても分からないものも存在する。分からない原則は頑張って理解しようとするより、一度忘れて 1 行でも多くコードを書くことを推奨する。今後コードを書いていて（もしくはサイト設計をしていて）うまくいかない箇所で詰まったとき、改めて原則のことを思い出すことで目指すべき指針を見つけられると思う。