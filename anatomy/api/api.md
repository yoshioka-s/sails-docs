# api/

apiフォルダにはSailsアプリの主要なロジックが含まれています。いわゆる<a href="https://ja.wikipedia.org/wiki/Model_View_Controller" target="_blank">MVCフレームワーク</a>におけるMとCが記述される場所です。

以下の内容が含まれます。

- コントローラ（Controllers）: ほとんどのバックエンドロジックが記載されます。
- ヘルパー（Helpers）: Sailsアプリ内のどこからでも呼び出すことのできる共通の処理のことです。
- モデル（Models）: アプリのデータを保持する構造を持ちます。
- ポリシー（Policies）: 主にユーザーの認証やアプリの一部へのアクセスを制御する必要がある場合に利用します。

以下のフォルダが存在する場合もありますが、自動で生成されるフォルダではありません。

- レスポンス（Responses）: サーバーレスポンスのロジックです(詳細は[カスタムレスポンスについて](http://sailsjs-org.com/documentation/concepts/extending-sails/custom-responses)を参照)
- サービス（Services）: サービスはSail 1.0以前に作成された共通処理のことを示します。Sails 1.0では_ヘルパー_を利用することが推奨されます。


<docmeta name="displayName" value="api">

