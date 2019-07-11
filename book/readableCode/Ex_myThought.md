# 自分の考え方
リーダブルコードの資料内で問いかけた設問に対する自分の考えです<br>
考え方が間違っていたり一般的でない考え方をしていると思ったときは是非反応をください

## README
### 設問：あなたはどちらのコードがより優れていると思いますか？
まず、どちらが優れているか絶対の解は存在しません（コードの美しさ参考）<br>
そのうえでどちらが良いかを述べます

コードを読む場合など、人間が覚えておける瞬間記憶の量には限界があります<br>
そのため一瞬一瞬で脳内に記憶する要素が少ない程理解しやすいコードだと考えます<br>

設問のコード内で認識する必要がある要素は<br>
・三項演算子は「判定」「処理A」「処理B」の1行に3つ<br>
・if文は1行目で「判定」、2行目で「処理A」（存在すれば3行目に「処理B」）の各行に1つずつ<br>
です<br>
今回の例では脳のリソースが少ない、後者の「if文」が良い書き方であると考えます

※上記の理由から三項演算子は「脳のリソースを多く使う、使い方を限定すべき」書き方だと考えています

## 美しさ
### 設問：適切な改行・インデントを入れることで視認性をあげてください

```HTML
<ul>
    <li>
        <h4>結月ゆかり</h4>
        <p>AHS社商標登録商品である</p>
        <b>ボイスロイド</b>
        <b>ボーカロイド</b>
        <p>です。</p>
    </li>
    <li>
        <h4>輿水幸子</h4>
        <p>自信満々で、自分が一番可愛いと信じて一直線に生きている女の子です。</p>
    </li>
    <li>
        <h4>UNISON SQUARE GARDEN</h4>
        <p>メンバー自身が誰よりも音楽を楽しんでいるバンドです。</p>
    </li>
</ul>
```

### 設問：下記のCSSを「段落」と「意味のある並び」をもたせて書き直しなさい

```CSS
.btn_wrap {
    display: flex;
    width: 700px;
}
.btn {
    width: 300px;
    height: 100px;
    backglound-color: white; /* 初期設定 */
}
.btn-blue {
    backglound-color: green;
}
.btn-green {
    backglound-color: green;
}
.btn_text {
    font-size: 1.2em;
    margin-bottom: 0px;
}
```

### 設問：あなたはインデントを修正しますか？混在したまま書きますか？

> コーディングは、「正しく書く」よりも「一貫性を持って書く」方が重要です。

上記より、インデントを踏襲してコーディングする<br>
（もし余裕があればコーディングガイドラインを確認し、確認者に確認を取ってから修正する）
## 思いやり
### 設問：タブ機能を実装したJavaScriptをリファクタリングしてください

```JavaScript
/**
 * タブがクリックされたとき対応するコンテンツを開くイベント
 * @param  {context} currentTab eventを発火したタブ自身
 * @param  {string}  targetID   開くコンテンツのid
 */
const openTab = function (currentTab, targetID) {
    // クリックされたときに開いているタブとコンテンツは一度全て閉じる
    delteAllClass('.tabs', 'js-openTab');
    delteAllClass('.content', 'js-openContent');

    // クリックされたタブのコンテンツを開く
    const targetContent = document.getElementById(targetID);
    targetContent.classList.add('js-openContent');
    currentTab.classList.add('js-openTab');
};

/**
 * 指定された要素が渡されたクラス名を保持している場合削除する
 * @param  {string} selectorName
 * @param  {string} delClassName
 */
const delteAllClass = function (selectorName, delClassName) {
    const targets = document.querySelectorAll(selectorName);
    targets.forEach((target) => {
        target.classList.remove(delClassName);
    });
};
```

## 命名
### 設問：適切な命名をしてください

1. clickNav()
1. addClassName(target, className)
1. .text-preWrap

### 設問：下記の関数名や引数、返り値を適切な命名へ修正しなさい

```JavaScript
/**
 * 天気の情報を取得する関数
 * @param  {strign} 情報を取得したいエリアID
 * @return {array}  取得結果
 */
const fetchWeatherData = function (areaID) {
    // body...
    return fetchData;
}
```

### 設問：下記の命名に対応する名前を考えてください

- rangeEnd
- endEvent()
- .btn-hidden

## コメント
### 設問：上記例から1つ選び、コードと共にダメなコメントを答えてください。さらにダメなコメントを改善したコメントを答えてください
提出コードのコメントを読み、修正後が改善されているか確認する

### 設問：下記の関数にJSDocのフォーマットでコメントしてください

```JavaScript
/**
 * 渡された数値を足した結果を返す関数
 * @param  {Number} num1
 * @param  {Number} num2
 * @return {Number} sum
 */
const sumCount = function (num1=0, num2=0) {
    /**
     * 引数を足した数
     * ※引数の型チェックを行わないため、Stringsが渡された場合はStringsになる
     */
    const sum = num1 + num2;

    return sum;
};
```

## ロジック
### 設問：if文を並び替えてください

```JavaScript
if (/* よくあるケース */) {
    // メイン処理
} else if (/* 上記と同じ頻度の特殊ケース */) {
    // 軽い処理A
} else if (/* 上記と同じ頻度の特殊ケース */) {
    // 軽い処理B
} else /* 特殊ケース */ {
    // 長い処理
    // 長い処理
    // 長い処理
}
```

### 設問：リファクタリングしてください

```JavaScript
const data = [14,21,73,43,9,45];
const count = data.lenght;
const now = new Date();
const today = now.getDate();
let num = [];

for (var i = count; i < count; i++) {
    if ((data[i] > 31) && (data[i] < today)) {
        continue;
    }
    num.push(data[i]);
}
```

