# api/controllers/UserController.js

このファイルは、`sails generate controller user`または`sails generate api user`を実行することで生成されます。なお、このコマンドは同時に[Userモデル](http://sailsjs-jp.org/documentation/anatomy/api/models/user.js)も生成します。

ここには&ldquo;コントローラ・アクション&rdquo;を記述します。コントローラ・アクションは、クライアントにデータを送信し、そのデータを表示するビューを描画します。

典型的には`/user/`で始まるURLにルーティングして、Userコントローラ内のアクションを実行します。ルーティング設定は[`config/routes.js`](http://sailsjs.com/documentation/anatomy/config/routes.js)で手動で記述することも可能ですが、[blueprintルート（blueprint routes）](http://sailsjs-jp.org/documentation/concepts/blueprints/blueprint-routes)に依存することで自動で設定することも可能です。

<docmeta name="displayName" value="UserController.js">
