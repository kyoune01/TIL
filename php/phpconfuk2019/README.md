---
title: "phpconfuk2019"
slug: "/reading/phpconfuk2019"
date: "2003-02-00"
---

## 開催情報

[PHP カンファレンス福岡 2019](https://phpcon.fukuoka.jp/2019/)  
2019.6.29(sat) 10:00 - 18:00  
福岡ファッションビル 8 階 A・B・C・D ホール

## PHP 型検査

スライド

- PHP の型検査は難しい
- 無理くり型を書くなら書くな
- PHPDoc 書け
- CI で型チェックしたい
- array → string[] 書き方知らなかった
- function X(): void 書き方知らなかった
- スライドをゆっくり拝見したい

## Monitoring PHP

[スライド](https://slide.seike460.com/slides/phpconfuk2019#/)

- 守りと攻めのモニタリング → 機会損失を防ぐ意味と次の改善を促す（Google Analytics みたい）
- PHP 側で関係するのは　応答数、メモリ使用量、CPU 使用量　など
- データを pull するか push するか 2 種類の監視方法がある
- モニタリングは思考のレベルが辿り着いてない感があった

## Web サービスの成長を止めずにリファクタリングする技術

[スライド](https://speakerdeck.com/soudai/web-refactoring)

- リファクタリングしてない
- web サービスは稼働と一緒に進化も止めない
- チーズ → 見たくはないがないと困るコード
- 腐った牛乳 → コメントアウトされた Cake1 時代のコード（まったく必要ない）
- 機能追加＋バグ修正 → 振る舞いが変わる
- 最適化＋リファクタリング → 振る舞いが変わらない（多分直近で必要なのはこっち）
- 絶対に上記を混ぜた課題を建てない（テストの内容が変わる → テストの内容を絞れる？）
- 絶対にゴールを決める
- リファクタリング要件
  - 新機能とコンフリクトしない
  - 振る舞いを替えない
  - サービスを止めない
  - 新たな負債を作らない
- 機能が分けられない状態なら分けるのが始めのリファクタリング
- 振る舞いを替えない → 振る舞いが変わってないことを証明する
- テストを書け
- 「いい方法が浮かばない…」「大きすぎて時間が足りない…」 → リファクタリングしない（大事）
- シナリオテストは最近導入された、ユニットテストはしてない（できる状態じゃない）
- シナリオをいきなり自動化しない（耳が痛い）
- テーブル設計に不具合、どうしようもない
- モデルがおかしい、これは決断がいるけどできたらもっと model がスリムになりそう
- FatController なので Service 層を導入したのは良かった
- 状況によるけれど同 FW 内で API を呼ぶ設計なのは冗長すぎる気がする
- View に if 文は沢山書いてきた
- Service 層で View で出力する内容を準備する？ → ここの想像がうまくできない
- 一番自分の環境に近い発表で学びが多かった

## 古き良き開発現場に新しい環境を作ろう！

[スライド](https://speakerdeck.com/nako0123/lets-create-a-new-culture-in-the-old-development-site)

- まずはドキュメントの整理は自分もやってきた → その後の発言力アップはできてない
- Backlog 優先で処理するって周りの意識作りが成功してるので、その意識作りが気になる
- 手順書 → 仮想環境、これは自分の仕事なのでやらないと
- markdown の書き方勉強会したい
- 仲間を増やしたい → 時々やる無理しない
- 自分も頑張ろうと思える感じの内容だった

## ユニットテストの現場の問題を原則に立ち返って考える

[スライド](https://speakerdeck.com/hgsgtk/think-deep-unit-test-practical-problem)

- ユニットテストをちゃんとしようと思ったところに良い流れでありがたい…
- 手動テストと自動化テスト
- ユニットテストによるコスト削減 vs ユニットテストの作成・維持のコスト
- テストから一目で理解できなければ負債
  - コメントいれよう？
- ちゃんとお前らエラーハンドリングせんやろ？アサートいらんやろ？（耳が痛い）
  - エラーコメントは「 f(x) = y, want z 」の形で出力しろ
- 実行順序で結果が変わるテスト
- 追加したらわけわからんところでエラーになるテスト
  - ちゃんとグローバルはクリアしろ、フィクスチャレコード（？）を分けるか共通化するかちゃんとしろ
- 内部実装に依存したテスト
  - private なのが悪いって言ってたけれどうまく改善方法がわからんかった
- Mock 云々は本当に意味が理解できなかった、テストでも状態を変化させろ？

## クラウド環境化における API リトライ設計

[スライド](https://www.slideshare.net/ssuser537eef/api-152529773)

- SPA のリトライ処理は実装しなければ悩まなくていい（？）
- 考えないといけない処理だって感じだけれど、その前に SPA の FW 理解からしないと…

## PHPStan で CustomRule を作る

[スライド](https://speakerdeck.com/nazonohito51/make-phpstan-customrule-d596e237-6692-4e6b-b83b-f5fac3618797)

- CI ツール
- 個人開発なら PHPStorm、コードの品質保証で CI 仕込むならこっち
- カスタムルールが作れるようになる、というより静的解析ツールが内部でやってることの内容
- PHPStan 完全に理解した
- 1 ルール = 1 クラス
- 意味分解 → 構文解析 → AST へ変換
- node：クラスやメソッドの宣言文、scope：クラスやメソッドのコンテキスト、broker：外の状況も含めた解析者？
- 新規メソッドは戻り値引数の型宣言必須確認ルール欲しい
- ここでもやはり PHPDoc

## LT

いろいろ聞いたけれど理解できない内容と闇が深そうな内容がいくつかあった  
（オレオレパッケージとか）

### date()とか time()の関数より DateTime クラス使った方が良さそう的な話

スライド

- テストをちゃんとしてるならランタイム関数とか使わない当たり前だよなぁ
- Datetime より setNowDate()ができる Carbon
- cakephp では Chronos って名前

### Stripe+PHP でセキュアで安全な決済機能を作る

[スライド](https://speakerdeck.com/gorou_178/stripe-plus-phptesekiyuatean-quan-najue-ji-ji-neng-wozuo-ru)

- 情報漏えいの原因
  - クレジットカード情報を保持（一瞬でも保持しない）
  - アプリケーションが脆弱（耳が痛い）
- 情報の非保持化
  - 通過させない
  - 保存しない
  - 処理しない
- stripe でかいけつ！

### 知ると得するコマンドライン PHP の便利な使い方

スライド

- phpinfo.php は置いたままにしないでください（大事なことなので何度も言いました）
- でもコマンドたたけないなら置くしかない…
- でも php の cli と apache で見てる場所違うことあるよね？
