# CSS設計
- BEM
- OOCSS
- SMACSS
- FLOCSS
など

### 参考
各CSS設計手法を取り入れる上でのメリット・デメリットをまとめてみた
https://qiita.com/nezurika/items/a964e21d3596b0ee4c9a

BEMによるフロントエンドの設計 第1回 基本概念とルール
https://app.codegrid.net/entry/bem-basic-1



## BEM
- Block（塊）、Element (要素)、Modifier (修飾) の３つに分ける
- 命名規則は.block__element--modifierとする
- シングルクラス

メモ：細かな差分（背景色のみ）などはModifierで切り替えるが複数差分が存在する場合は、シングルクラスの考え方を優先してBlockを分ける

### コード例

```HTML
<ul class="executive">
  <li class="executive__item">
    <p class="executive__item__title"></p>
    <p class="executive__item__text"></p>
  </li>
</ul>
<ul class="profile">
  <li class="profile__item">
    <p class="profile__item__title"></p>
    <p class="profile__item__text"></p>
  </li>
  <li class="profile__item">
    <p class="profile__item__title"></p>
    <p class="profile__item__text"></p>
  </li>
</ul>
```

```CSS
.executive { ... }
.executive__item { ... }
.executive__item__title { ... }
.executive__item__text { ... }

.profile { ... }
.profile__item { ... }
.profile__item__title { ... }
.profile__item__text { ... }
```

## OOCSS
- 構造とスキン（見た目）を分離する
- オブジェクト指向
- マルチクラス

メモ：細かな差分（背景色のみ）などはModifierで切り替えるが複数差分が存在する場合は、シングルクラスの考え方を優先してBlockを分ける

### コード例

```HTML
<ul class="cardWrap">
  <li class="card w100 border-gold">
    <p class="title"></p>
    <p class="text"></p>
  </li>
</ul>
<ul class="cardWrap">
  <li class="card">
    <p class="title"></p>
    <p class="text"></p>
  </li>
  <li class="card">
    <p class="title"></p>
    <p class="text"></p>
  </li>
</ul>
```

```CSS
.cardWrap { ... }
.cardWrap.large { ... }
.cardWrap .card { ... }
.cardWrap .card .title { ... }
.cardWrap .card .text { ... }

.w100 { ... }
.border-gold { ... }
```

## SMACSS
- base/layout/module/state/themeの5つにわける
- layoutとstateとthemeには接頭語をつける
- マルチクラス

### コード例

```HTML
ul[class=""]>(li[class=""]>p[class=""]+p[class=""])
ul[class=""]>(li[class=""]>p[class=""]+p[class=""])*2
```

```CSS
```

## FLOCSS
- OOCSS, SMACSS, BEM, SuitCSS, MCSS の考え方を取り入れた比較的新しいやつ
- 命名規則はBEM
- マルチクラス

### コード例

```HTML
ul[class=""]>(li[class=""]>p[class=""]+p[class=""])
ul[class=""]>(li[class=""]>p[class=""]+p[class=""])*2
```

```CSS
```
