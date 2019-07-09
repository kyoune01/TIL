# コードの思いやり
リーダブルコードの目的である

**HTML・コードは他の人が最短時間で理解できるように書かなければならない**

を達成するために、コードの「思いやり」について説明していきます

## 1度に1つのことをする

ブラウザ上にトランプのデザインを実装しました。

```HTML
<ul class="cards">
    <li class="spade">3</li>
    <li class="heart">A</li>
    <li class="clover">J</li>
</ul>
```

```CSS
.cards {
    display: flex;
}
.cards .spade {
    margin-right: 10px;
    border: 1px solid #000;
    border-radias: 15px;
    background-color: #eee;
}
.cards .heart {
    margin-right: 10px;
    border: 1px solid #f00;
    ...
}
.cards .clover { ... }
```

上記のように基本の中身をコピペでCSSを書いた場合「角のカーブをもっと小さくしたい」などのデザイン修正がはいった場合に全てのクラスへ修正が発生します

コピペしたことが原因ではありません。「基本デザイン」「個別デザイン」を１つのCSSセレクタで実装したことが原因です

次に「基本デザイン」「個別デザイン」を分割したCSS設計で実装しました

```HTML
<ul class="cards">
    <li class="card_item card_item-spade">3</li>
    <li class="card_item card_item-heart">A</li>
    <li class="card_item card_item-clover">J</li>
</ul>
```

```CSS
.cards {
    display: flex;
}
.cards .card_item {
    margin-right: 10px;
    border-radias: 15px;
    border: 1px solid #fff; /* 初期値 */
    background-color: #fff; /* 初期値 */
}
.cards .card_item-spade {
    border: 1px solid #000;
    background-color: #eee;
}
.cards .card_item-heart { ... }
.cards .card_item-clover { ... }
```

このCSSなら「card_item => 基本デザイン」「card_item-〇〇 => 個別デザイン」が分離していてメンテナンスが簡単になりました

1つの役割に沢山の機能が含まれる、1：多のCSS・コードは破綻しやすいです。それより1：1に保つ方が他人が読んでも理解しやすく、メンテナンスもしやすいです<br>
※ただし分割しすぎると多：1の関係になるので注意が必要

## 役割を明確に説明する

先程はCSSを「基本デザイン」「個別デザイン」に分けました。十分メンテナンスはしやすくなりましたが、さらに踏み込んで「役割」で分割します

```HTML
<ul class="l-container-12">
    <li class="l-grid-4">
        <div class="card card-spade">
            <p class="card-text">3</p>
        </div>
    </li>
    <li class="l-grid-4">
        <div class="card card-heart">
            <p class="card-text">A</p>
        </div>
    </li>
    <li class="l-grid-4">
        <div class="card card-clover">
            <p class="card-text">J</p>
        </div>
    </li>
</ul>
```

役割で分割することで「l-container-12 => グリッドデザイン用のラッパー」など、「各クラスが何のために存在しているか」を一言で説明できるようになりました<br>
※しかし先ほど述べた通り、分割したことによって更にHTMLへの負荷が上がりました。どのレベルまで分割するか案件やサイト規模を考慮して、どのCSS設計を選択するか判断してください

またCSSだけでなく、Javascriptで機能を実装しているときにも必ず1つの目的があります。目的を言葉で説明できない状態、説明以外のことをしている状態を避けましょう

<br>
設問：タブ機能を実装したJavascriptをリファクタリングしてください。必要な動作は下記です

- クリックされたときにタブが開いていた場合、全て閉じる
- クリックされたタブのコンテンツを開く

```HTML
<ul>
    <li class="tabs js-openTab" onClick="openTab(this, 'content1')">tab1</li>
    <li class="tabs" onClick="openTab(this, 'content2')">tab2</li>
    ...
</ul>

<div class="contentWrap">
    <div id="content1" class="content">...</div>
    <div id="content2" class="content">...</div>
    ...
</div>
```

```Javascript
const openTab = function (currentTab, targetID) {
    const tabElement = document.querySelectorAll('.tabs');
    tabElement.forEach((tab) => {
       tab.classList.remove('js-openTab');
    });
    const contentElement = document.querySelectorAll('.content');
    contentElement.forEach((content) => {
        content.classList.remove('js-openContent');
    });

    currentTab.classList.add('js-openTab');

    const targetContent = document.getElementById(targetID);
    targetContent.classList.add('js-openContent');
};
```

<br>

## ライブラリを知る
ライブラリを知っていればもっと短く簡潔にかけます<br>
普段から具現化系能力者のごとくライブラリに親しむことが大事です

Before

```Javascript
const openTab = function (currentTab, targetID) {
    const tabElement = document.querySelectorAll('.tabs');
    tabElement.forEach((tab) => {
        tab.classList.remove('js-openTab');
    });
    const contentElement = document.querySelectorAll('.content');
    contentElement.forEach((content) => {
        content.classList.remove('js-openContent');
    });

    currentTab.classList.add('js-openTab');

    const targetContent = document.getElementById(targetID);
    targetContent.classList.add('js-openContent');
};
```

After

```Javascript
const openTab = function (currentTab, targetID) {
    const $tabElement = $('.tabs');
    $tabElement.removeClass('js-openTab');

    const $contentElement = $('.content');
    $contentElement.removeClass('js-openContent');

    $(currentTab).addClass('js-openTab');

    const $targetContent = $(targetID);
    $targetContent.addClass('js-openContent');
};
```

## 短いコードを書く

コーダー・エンジニアが目指すべき、万人が読めるコードは「何も書かないこと」です

```Javascript
// やって欲しいことが何も書かなくても実行される
```

しかし残念なことに物理現象や保存則のせいで無から有はつくれません。できるだけ万人が読めるコードを目指して「短く」「簡単な」コーディングを行いましょう<br>
またブラウザの読み込みやレンダリングは早い方が体験が向上します。実際の案件でも短いコードを書けること、短いコードに変換できることは必須の技術です

今後、読みやすいコーディングで心がけたいこととして下記を意識してください

- 重複したコードを生み出さないために、汎用的で多目的に使えるコードを書く
- 使われていないコードや役に立たない機能は削除する

## まとめ

少し言語特性によった内容になりましたが、本ドキュメントで伝えたいことは下記です。意識しなくても実行できる状態を目指しましょう

- 1つの処理は1つのことだけをする
- ライブラリを知る
- 短くコードを書く（コードを役割で分割する）
