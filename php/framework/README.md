# フレームワーク
- Laravel
- cakephp
- codeigniter
- Symfony
- Smarty

### 参考
- [CakePHPとLaravelの比較2018](https://crieit.net/posts/CakePHP-Laravel-2018)
- [【徹底比較】2019年版PHPフレームワークおすすめランキングTOP5](https://www.sejuku.net/blog/4016)

## Laravel
[公式HP](https://laravel.com/)

- 超有名＋開発が楽しいFW
- ディレクトリが煩雑で散らばってるイメージ
- デフォルトでVueが入ってるなど、フロント側との連携がしやすい
- cakeのBake的なartisan
- viewはBlade、ValidationはControllerに書く

デフォルト

```
Laravel/
    ├── app/
    │   ├── Http/
    │   │   ├── Controller/ // コントローラ
    │   │   └── Middleware/ // ミドルウェア
    │   └── models/         // モデル
    ├── config/             // DB、appなど各種設定
    ├── datebase/
    │   ├── migrations/     // テーブルを簡単につくれる
    │   └── seeds/          // テーブルに値を簡単に入れられる
    ├── resources/
    │   ├── assets/         // sassやSPA-Vueなどサーバ側で動作するリソース
    │   │   ├── sass/
    │   │   └── js/
    │   └── views/          // ビュー
    ├── routes/
    │   ├── web.php         // ページ用ルーティング
    │   └── api.php         // API用ルーティング
    └── tests/              // テスト置き場
```

## cakephp
[公式HP](https://cakephp.org/jp)

- 綺麗なMVC規約、規約がすべて
    - Model、View、Controller、役割が全てディレクトリ名なので初心者がとっつきやすい（と思う）
- 使用感は他FW（Laravel）と同じ
- Vueなどの連携がない
- Bakeコマンドで各ファイルを生成できる
- routingファイルが1つなのでAPIと分けたいときにめんどくさいかも
- 「AppController.php」など全ての役割毎に継承元の「App」ファイルが存在する

デフォルト

```
cakephp/
    ├── config/
    │   ├── app.php         // FWの全体設定
    │   ├── env.php         // 環境設定
    │   └── routes.php      // ルーティング
    ├── pulgins/
    ├── tests/              // テスト置き場
    ├── tmp/
    │   └── cache/          // キャッシュ置き場
    ├── logs/
    │   ├── debag.log       // デバッグ出力先
    │   └── error.log       // エラー出力先
    └── src/
        ├── Controller/     // コントローラ、ページのメイン処理
        │   └── Component/  // コントローラの共通処理置き場
        ├── Model/          // モデル
        │   ├── Behavior/   // ビヘイビア
        │   ├── Entity/     // DBとやり取りするために条件を整理する場
        │   └── Table/      // DBと直接やり取りする場
        ├── Template/       // コントローラに対応した実際のビュー置き場
        └── View/           // ヘッダーなど共通化できるパーツ置き場
            └── Helper/     // ヘルパー
```

デフォルトの構成に追加した層

```
cakephp/
    ├── config/
    │   └── routes_api.php  // API用ルーティング
    │                               通常のルーティングと分ける
    ├── Service/            // 各コントローラから処理を分離したメソッド置き場
    │                               処理を分離してFatControllerを防ぐ
    └── src/
        └── Model/
            └── Validate/   // 共通バリデーションルール置き場
```

何も知らなくても最低限抑えるべき場所

```
cakephp/
    ├── config/
    │   ├── app.php         // FWの全体設定
    │   ├── env.php         // 環境設定
    │   └── routes.php      // ルーティング
    ├── tmp/
    │   └── cache/          // とりあえずキャッシュ削除して再読込
    ├── logs/
    │   └── error.log       // エラー内容が書かれてる
    └── src/
        ├── Controller/     // ルーティング情報からここを探す
        ├── Model/
        │   └── Table/      // DBのテーブル情報
        └── Template/       // ブラウザで表示される内容はここ
```

## codeigniter
[公式HP](https://www.codeigniter.com/)

- パフォーマンスが良い、ただしFWの恩恵は少ない
- コア部分の処理が追いやすい
- 記事は2015～2017年までの記事が多い印象
- composer 対応

デフォルト（composer kenjis使用）

```
codeigniter/
    ├── bin(system)/        // コアファイル
    └── application/
        ├── config/         // 各設定
        │   └── routes.php  // ルーティング
        ├── controllers/    // コントローラ
        ├── models/         // モデル
        └── views/          // ビュー
```

## Symfony
[公式HP](https://symfony.com/legacy)

- ドメイン駆動設計を推奨（modelがない）
- サーバインストールで動く、ファイル納品だけでは動かない？

> 比較的規模の大きなWebサービスがSymfonyで作られています<br>
> アプリケーションを開発する上で開発と保守を効率化することを目的とし

らしい

## Smarty
[公式HP](https://www.smarty.net/docsv2/ja/)

- HTMLテンプレートを使用していた時代に主流だった
- PHP4 から対応
- composer 未対応
- いま新規フレームワークとして選ぶ理由は何もない
- ロジックとビューに分け、ロジック部分をキャッシュとして吐き出すため高速に読み込みができた