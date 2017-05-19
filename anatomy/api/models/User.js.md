# api/models/User.js

このファイルは`sails generate model user`または`sails generate api user`のコマンドを実行することで生成されます。なお、この際、[Userコントローラ](http://sailsjs.com/documentation/anatomy/api/controllers/UserController.js)も合わせて生成されます。

このファイルでは、それぞれのモデルのレコードがどのような性質を持つべきか定義します。また独自のモデルクラスメソッドの定義や`datastore`のようなグローバルな設定内容の上書きも可能です。

Sailsの良いところの一つは[Waterline](https://github.com/balderdashy/waterline)というORMを利用する点です。このため、データベースの選択を可能な限り遅らせたまま、モデルの開発を進めていくことが可能です。


<docmeta name="displayName" value="User.js">
