# lint

## 概要

静的解析を行うための「linter」と各言語のコーディング規約の紹介を行う
合わせてコードフォーマットを行う「prettier」を紹介する

## linter・prettierとは

構文エラーや使用されていない変数の検知などをチェックする処理（プログラム）を「lint」  
プログラムが動くパッケージを「linter」と呼ぶ  
linterの中で、コードフォーマットのみを行うパッケージの1つとして「prettier」が存在する

linterでは構文チェック、prettierではコード整形をおこなうため異なる役割をもつ

## 使用するメリット

前提として、コーディング規約を人間が完全に守るのは難しく、規約を守られていないコードは読み辛くなり不具合を生むことが知られている

linter・pretterを通すことで、下記のようなメリットがある

- 公開前に事前にエラーを検知できる  
→ テストの手戻り工数を削減
- 規約を意識せずに実装へ集中できる  
→ 実装すべき処理・コーディングへ集中できる
- レビュー・調査時に不要な脳のリソースを使用しない  
→ 新卒・既卒関わらず一定の品質を担保できる

## 設定方法

設定方法によっていくつか動作タイミングがある  
基本はローカルで動作させ「皆が見える場所へファイルを上げる前に確認する」

注意点としてどのlinter/prettierもパッケージとして配布されているため、パッケージを理解していることが前提となる

### 保存したら動作

エディターでファイルの保存時に自動で実行する

例：vscode prettier  
[VSCode でファイル保存時にPrettierに自動整形してもらう](https://qiita.com/ezawa800/items/e6352948b654ba5981cf)

### コミット・プッシュ前に動作

[git hook](https://git-scm.com/book/ja/v2/Git-%E3%81%AE%E3%82%AB%E3%82%B9%E3%82%BF%E3%83%9E%E3%82%A4%E3%82%BA-Git-%E3%83%95%E3%83%83%E3%82%AF) を用いる  
※hook ファイルへ直接書く方法は開発者の環境に依存するため、「npm package」を導入している案件であれば「husky」も提案する

例：husky linter  
[gitのイベントをフックして自動lintをかける](https://qiita.com/daisukeoda/items/3b9a31b235e9fd5393c8)

## 各言語によるコーディング規約

最後にlinterがなにを正とするか、各言語で使用されているモダンな規約を紹介する

- html、CSS：[Google HTML/CSS Style Guide まとめ](https://qiita.com/Sugima/items/785644372397595644ba)  
※記事内参照元：[Google HTML/CSS Style Guide](https://google.github.io/styleguide/htmlcssguide.html)
- js：[JavaScriptのスタイルガイドまとめ(おすすめ4選)](https://qiita.com/takeharu/items/dee0972e5f39bfd4d7c8)
- php：[PHPコーディング規約まとめ](https://qiita.com/hshimo/items/04be1f432240c58300f4)  
※記事内参照元：[PSR-2: Coding Style Guide](https://www.php-fig.org/psr/psr-2/)
- python：[PEP: 8](https://pep8-ja.readthedocs.io/ja/latest/)
