# コードの美しさと思いやり
リーダブルコードの目的である

**HTML・コードは他の人が最短時間で理解できるように書かなければならない**

を達成するために、このドキュメントでは言語にかかわらない  
コードの「美しさ」と「思いやり」について説明していきます

## 美しさ
この章から、読みやすさに大きな比重を占める視認性について記載していきます

### なぜ美しさが大事なのか
ではさっそく、下記のHTMLは修正しやすいでしょうか？  
内部にタブを一つ増やす指示を受けたとき3秒で対応できるかを想定して読んでみましょう

```HTML
<nav><ul id="tab" class="static"><li class="tabcon" id="tabcon1s"><p>tab1</p></li><li class="tabcon" id="tabcon2s"><p>tab2</p></li></ul></nav>
```

実際の業務ではパーサーを使うので問題として不適切？  
ではこのようなHTMLではどうでしょうか？  

```HTML
<nav><ul id="tab" class="static">
<li class="tabcon" id="tabcon1s">
<p>tab1</p>
</li>
    　    <li class="tabcon" id="tabcon2s"><p>tab2
</p></li><li class="tabcon" id="tabcon3s"><p>tab3</p></li>
</ul></nav>
```

実際の業務でみることがあれば頭を抱えそうな改行とインデントです  
しかし、このようなレイアウトを誰しも一度は見たことがあると思います（ない貴方は幸運です）  

人間はデザインの4大原則に基づいたコーディングを無意識のうちに綺麗だと感じます  
HTML・コードを書く際にはデザインの4大原則を意識することでおよそ綺麗な書き方ができます  

> デザインの4大原則  
> ・近接　・整列　・強弱　・反復  
> https://bulan.co/swings/design4principals/

次からは頭を抱えてしまうHTMLを副題に沿ってさらに読みやすくしていきます

### 改行位置とインデント
では先程の例で挙げた前者をよい書き方にしていきましょう  
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

これだけで十分読みやすくなりましたね  
適切な改行を与え頭を揃えることで意識して読みやすさをあげられます  
インデントを加えることでさらに読みやすくしてみましょう  

```HTML
<nav>
    <ul id="tab">
        <li class="tabcon" id="tabcon1s"><p>tab1</p></li>
        <li class="tabcon" id="tabcon2s"><p>tab2</p></li>
        <li class="tabcon" id="tabcon3s"><p>tab3</p></li>
    </ul>
</nav>
```

かなり読みやすくなりました  

なぜ改行とインデントを加えることで読みやすいと感じられるのでしょうか  
原理としてはデザイン4大原則の下記を用いているからです  

- 改行を入れることでタグをブロックレベルに「整列」する
- インデントをいれることで入れ子であることを「強調」する（仮想縦線を入れる）

これからはなんとなく改行・インデントを入れるのではなく、  
読みやすさを意識してHTML・コードを書いてみましょう。

- どのタグが入れ子になっているのか  
- 縦の線はどこにおくべきか  

<br>
<br>
設問：適切な改行・インデントを入れることで視認性をあげてください  

```
<ul><li><h4>結月ゆかり</h4><p>AHS社商標登録商品である</p><b>ボイスロイド</b><b>ボーカロイド</b><p>です。</p></li><li><h4>輿水幸子</h4><p>自信満々で、自分が一番可愛いと信じて一直線に生きている女の子です。</p></li><li><h4>UNISON SQUARE GARDEN</h4><p>メンバー自身が誰よりも音楽を楽しんでいるバンドです。</p></li></ul>
```

<br>
<br>

### 一貫性と意味のある並び
HTMLは記載の順で表示の順番が変わる、コードとは別のルールが存在します  
しかしJavascriptはコードの並び順がバラバラでもいい感じに動いてしまうためよくコードが混沌とします

例として、下記HTMLにタブで表示／非表示を切り替えるコードをあげます  

```HTML
<ul class="btn_wrap">
    <li class="btn btn-blue"><p class="btn_text">tab1</p></li>
    <li class="btn btn-green"><p class="btn_text">tab2</p></li>
</ul>
```

```Javascript
tab = document.getElementById('tabcon1s')
tab1.addEventListener('click',openTab);
tab = document.getElementById('tabcon2s')
tab3.addEventListener('click',openTab);
tab = document.getElementById('tabcon3s')
tab2.addEventListener('click',openTab);
```

上記のJavascriptのコードでは「段落」と「一貫性」が欠けた状態です。  

まずここでいう「段落」とは、似ている考えを1つにまとめて他の考えと分けたものを指します  
（デザイン4大原則でいう「整列」です）  

```Javascript
tab1 = document.getElementById('tabcon1s')
tab3 = document.getElementById('tabcon3s')
tab2 = document.getElementById('tabcon2s')

tab1.addEventListener('click',openTab);
tab3.addEventListener('click',openTab);
tab2.addEventListener('click',openTab);
```

つぎに「一貫性」とは、  
HTMLが「tab1」「tab2」「tab3」と並んでいる状態で、  
Javascriptが「tab1」「tab3」「tab2」と並んでおり同期がとれている状態を指します  

```Javascript
tab1 = document.getElementById('tabcon1s')
tab2 = document.getElementById('tabcon2s')
tab3 = document.getElementById('tabcon3s')

tab1.addEventListener('click',openTab);
tab2.addEventListener('click',openTab);
tab3.addEventListener('click',openTab);
```

<br>
<br>
設問：下記のCSSを「段落」と「一貫性」をもたせて書き直しなさい  

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
<br>

### 個人的な好みと一貫性・コーディングルール

皆さんはどちらのコードが優れていると思いますか？

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

結論を述べると、上記に答えは存在しません。しかし案件や仕事でどう対応をするべきか、には答えが存在します。  

- 業務のコーディングガイドラインに従うこと
- （既存のファイルを修正する場合）元々のファイルに揃えること

です。

どちらでコーディングを行ってもよいですが、両方が存在する場合、間違いなくコードを読む時間は増えます  
資料の初めに記載した

**HTML・コードは他の人が最短時間で理解できるように書かなければならない**

ために、どうやって書けばよいか考えられるとよいです。  

<br>
<br>
設問：既存ファイルを修正する際に、「Tab」インデントと「Space」インデントが混在している行を見つけました。  
　　　あなたはどうしますか？
<br>
<br>

## 思いやり
### 役割を明確に説明する
### ライブラリを知る
### 短いコードを書く
### コードを小さく保つ

## まとめ
自分の書いたコードが理解できない原因には  
・美しさと思いやりが足りない  
・長くて冗長である  
などの理由があることが意識できたと思います  

では短くて理解しやすくドライなコーディングをするにはどのような方法があるでしょうか？  
そのうちの一つの解として次回はCSSの命名／設計手法を紹介し、モジュールコンポーネントの作成を通じて実践を行います  
設計手法を用いることでどのようにコードを美しくできるか・短くできるかを意識してみてください  
お楽しみに～  