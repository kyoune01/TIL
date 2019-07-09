# コードの美しさ
リーダブルコードの目的である

**HTML・コードは他の人が最短時間で理解できるように書かなければならない**

を達成するために、コードの「美しさ」について説明していきます

## なぜ美しさが大事なのか
ではさっそく、下記のHTMLは修正しやすいでしょうか？<br>
内部にタブを一つ増やす修正指示を受けたと想定して3秒で対応できるか考えてみましょう

```HTML
<nav><ul id="tab" class="static"><li class="tabcon" id="tabcon1s"><p>tab1</p></li><li class="tabcon" id="tabcon2s"><p>tab2</p></li></ul></nav>
```

「実際の業務ではパーサーを使うので上記のようなコードを直接人間が修正することはない」？<br>
では下記のようなHTMLではどうでしょうか？

```HTML
<nav><ul id="tab" class="static">
<li class="tabcon" id="tabcon1s">
<p>tab1</p>
</li>
    　    <li class="tabcon" id="tabcon2s"><p>tab2
</p></li><li class="tabcon" id="tabcon3s"><p>tab3</p></li>
</ul></nav>
```

もし実際の業務で見ることがあれば、頭を抱えたくなる改行とインデントです<br>
しかし誰しも一度はこのようなレイアウトを見たことがあると思います（ない貴方は幸運です）

### 美しさとは
人間はデザインの4大原則に基づいたコーディングを無意識のうちに綺麗だと感じます<br>
HTML・コードを書く際にはデザインの4大原則を意識することで綺麗な書き方ができます

> デザインの4大原則  
> ・近接　・整列　・強弱　・反復  
> https://bulan.co/swings/design4principals/

次からは頭を抱えてしまうHTMLを副題に沿って読みやすく、美しく修正していきます

## 改行位置とインデント

まずは副題に沿って適切な改行をHTMLへ与えます

```HTML
<nav>
<ul id="tab" class="static">
<li class="tabcon" id="tabcon1s"><p>tab1</p></li>
<li class="tabcon" id="tabcon2s"><p>tab2</p></li>
<li class="tabcon" id="tabcon3s"><p>tab3</p></li>
</ul>
</nav>
```

これだけで十分読みやすくなりましたね<br>
適切な改行を与え頭を揃えることで意識して読みやすさをあげられます<br>
ここにインデントを加えることでさらに読みやすくしてみましょう

```HTML
<nav>
    <ul id="tab">
        <li class="tabcon" id="tabcon1s"><p>tab1</p></li>
        <li class="tabcon" id="tabcon2s"><p>tab2</p></li>
        <li class="tabcon" id="tabcon3s"><p>tab3</p></li>
    </ul>
</nav>
```

十分読みやすくなりました

では、なぜ改行とインデントを加えることで読みやすいと感じられるのでしょうか<br>
原理としてはデザイン4大原則の下記を用いているからです

- 改行を入れることでタグを「整列」する
- インデントをいれることで入れ子であることを「強調」する（仮想の縦線を引く）

これからはなんとなく改行・インデントを入れるのではなく、読みやすさを意識してHTML・コードを書いてみましょう。

<br>
設問：適切な改行・インデントを入れることで視認性をあげてください<br>

```
<ul><li><h4>結月ゆかり</h4><p>AHS社商標登録商品である</p><b>ボイスロイド</b><b>ボーカロイド</b><p>です。</p></li><li><h4>輿水幸子</h4><p>自信満々で、自分が一番可愛いと信じて一直線に生きている女の子です。</p></li><li><h4>UNISON SQUARE GARDEN</h4><p>メンバー自身が誰よりも音楽を楽しんでいるバンドです。</p></li></ul>
```

<br>

## 一貫性と意味のある並び

下記HTMLにタブで表示／非表示を切り替えるコードをあげます<br>
Javascriptの処理を一瞬で理解できるでしょうか？

```HTML
<ul class="btn_wrap">
    <li class="btn btn-blue"><p class="btn_text">tab1</p></li>
    <li class="btn btn-green"><p class="btn_text">tab2</p></li>
</ul>
```

```Javascript
tab1 = document.getElementById('tabcon1s');
tab1.addEventListener('click',openTab);
tab3 = document.getElementById('tabcon3s');
tab2 = document.getElementById('tabcon2s');
tab2.addEventListener('click',openTab);
tab3.addEventListener('click',openTab);
```

上記のJavascriptのコードは「段落」と「意味のある並び」が欠けた状態です。「段落」と「意味のある並び」を与えることでコードの可読性を上げていきます

まずはコードに「段落」を与えます。「段落」とは、似ている考えを1つにまとめて他の考えと分けたものを指します<br>
（デザイン4大原則の「整列」「反復」です）

```Javascript
tab1 = document.getElementById('tabcon1s');
tab3 = document.getElementById('tabcon3s');
tab2 = document.getElementById('tabcon2s');

tab1.addEventListener('click',openTab);
tab3.addEventListener('click',openTab);
tab2.addEventListener('click',openTab);
```

つぎに「意味のある並び」を与えます。「意味のある並び」とは「1,2,3...」や「a,b,c...」などの要素が並んでいるとき、次は◯◯が来て欲しいなど、「こうであって欲しい順番」を指します。

```Javascript
tab1 = document.getElementById('tabcon1s');
tab2 = document.getElementById('tabcon2s');
tab3 = document.getElementById('tabcon3s');

tab1.addEventListener('click',openTab);
tab2.addEventListener('click',openTab);
tab3.addEventListener('click',openTab);
```

はじめのコードより理解に必要な時間が大幅に削減することができましたね

HTMLは記載の順で表示の順番が変わるため、コードとは別のルールで記載します<br>
しかしJavascriptはコードの並び順がバラバラだとしても想定通りに動いてしまうため、長期期間運用されてきたコードでは混沌とすることが多いです

自分がどの段落を修正すべきか、修正したことで意味の並びが変わらないか意識して修正することが重要です

<br>
設問：下記のCSSを「段落」と「意味のある並び」をもたせて書き直しなさい<br>

```HTML
<ul class="btn_wrap">
    <li class="btn btn-blue"><p class="btn_text">tab1</p></li>
    <li class="btn btn-green"><p class="btn_text">tab2</p></li>
</ul>
```

```CSS
.btn_text {
    font-size: 1.2em;
    margin-bottom: 0px;
}
.btn {
    width: 300px;
    height: 100px;
    backglound-color: blue;
}
.btn-green {
    width: 300px;
    height: 100px;
    backglound-color: green;
}
.btn_wrap {
    display: flex;
    width: 700px;
}
```

<br>

## 個人的な好みと一貫性・コーディングルール

皆さんはどちらのHTMLが優れていると思いますか？

```HTML
<p>
    <span>tab1</span>
</p>
```

```HTML
<p><span>tab1</span></p>
```

もしくは下記のコードの場合、どちらが視認性が良いでしょうか？

```Javascript
if (isChecked) {
    return true;
}
```

```Javascript
if (isChecked)
{
    return true;
}
```

結論を述べると、上記に答えは存在しません<br>
しかし「案件や仕事でどう対応をするべきか」の場合は答えが存在します。

- 業務のコーディングガイドラインに従うこと
- （既存のファイルを修正する場合）元々のファイルに揃えること

です。

どちらでコーディングを始めてもよいですが、ファイルに異なるルールが存在する場合は間違いなくコードを読む時間が増えます

コーディングは、「正しく書く」よりも「一貫性を持って書く」方が重要です。

<br>
設問：既存ファイルを修正する際に、「Tab」インデントと「Space」インデントが混在している行を見つけました。あなたはインデントを修正しますか？混在したまま書きますか？
<br>
<br>


## まとめ

HTMLを書く際に美しさを意識することで、理解に必要な時間を削減できる例を記載しました<br>
実際のコーディングではエディタの補完機能を用いてコーディングしていくと思います

しかし、コーダ・エンジニアとして生きるために、開発環境の設計などルールを決める場でなぜそのルールが必要なのかについて意識できる、未来の負債にならないような修正方法を意識できるようになってください

最後に、
**Javascriptの末尾「;」を付けるか付けないかは必ず統一しなさい**
