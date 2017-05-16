# Application (`sails`)

Sailsのapplicationオブジェクトは、Sailsアプリケーションに必要な全てのruntime stateを含んでいます。
デフォルトでは、'sails'としてグローバルに利用可能ですが、この機能を [オフにすることが可能](http://sailsjs-jp.org/documentation/reference/configuration/sails-config-globals)です。例：複数のSails appインスタンスが必要な場合やglobal変数が許可されていない場合など。
applicationオブジェクトはリクエストにおいては`req.sails`、[モデル](http://sailsjs-jp.org/documentation/concepts/models-and-orm/models)内、そして[サービス](http://sailsjs-jp.org/documentation/concepts/services)モジュールでは`this.sails`を用いていつでもアクセスすることが可能です.

> 通常は`sails` applicationオブジェクトについては、基本的ないくつかのメソッドと、カスタム設定について知っていれば十分です。より高度な機能については[高度な機能](http://sailsjs-jp.org/documentation/reference/application/advanced-usage)セクションで知ることができます。

### 仕組み

applicationインスタンスは最初に`require('sails')`した瞬間に生成されます。
これは自動生成された`app.js`ファイル内の

```javascript
var sails = require('sails');
```

において行われていることです。

### プロパティ（Properties）

applicationオブジェクトはたくさんの有益なメソッドやプロパティを有しています。
`sails`オブジェクトの全解説は他のページに記載されていますが、以下はいくつかの有益なプロパティの例です。

##### sails.models

_identity_ にてインデックスされた、全てのロード済み[Sailsモデル](http://sailsjs-jp.org/documentation/concepts/models-and-orm/models)を持つ連想配列です。

デフォルトでは、モデルのファイル名から**.js**を除いた小文字をモデルの名称（_identity_）としています。例えば、`api/models/PowerPuff.js`からロードされたモデルの名称（_identity_）は`powerpuff`となり、`sails.models.powerpuff`でアクセスが可能になります。モデルの名称（_identity_）はそのモデルのmodule fileから`identity`プロパティを設定することで変更できます。

##### sails.config

環境変数、`.sailsrc`、user-configurationファイルとdefaultsからロードされたsailsインスタンスに適用される全ての設定オプションです。
[設定](http://sailsjs-jp.org/documentation/concepts/configuration)にSailsにおける設定方法の概要が、[設定レファレンス](http://sailsjs-jp.org/documentation/reference/configuration)に各設定オプションの詳細を解説しています。

##### sails.sockets

websocketを取り扱う上での便利なメソッドを提供しています。
詳細は、[`sails.sockets.*`レファレンス](http://sailsjs-jp.org/documentation/reference/web-sockets/sails-sockets)に記載しています。

##### sails.hooks

_identity_ にてインデックスされた、全てのロード済み[Sails hooks](http://sailsjs-jp.org/documentation/concepts/extending-sails/hooks)を持つ連想配列です。
`sails.hooks`を用いることで、Sailsに追加インストールした様々なプロパティやメソッドを利用できます。例えば、`sails.hooks.email.send()`など。この連想配列を利用することで、Sailsの[core hooks](http://sailsjs-jp.org/documentation/concepts/extending-sails/hooks#?types-of-hooks)も利用できます。

デフォルトでは、hookの名称（_identity_）は`sails-hook-`prefixを除いたフォルダ名の小文字表記になります。例えば、`node_modules/sails-hook-email`からロードされたhookのアイデンティティは`email`となり、`sails.hooks.email`からアクセス可能になります。インストール済みのhookの名称（_identity_）は[`installedHooks`コンフィグ・プロパティ](http://sailsjs-jp.org/documentation/concepts/extending-sails/hooks/using-hooks#?changing-the-way-sails-loads-an-installable-hook)から変更できます。

[hooksのコンセプト](http://sailsjs-jp.org/documentation/concepts/extending-sails/hooks)にhookについて詳細を解説しています。

##### `sails.io`

[`sails.sockets.*` methods](http://sailsjs-jp.org/documentation/reference/web-sockets/sails-sockets)の提供するAPIはほとんどのアプリケーションの開発に耐え得る内容であり、webscocketの内部的な仕様の変化を覆い隠す力がありますが、レガシーなSocket.ioベースのアプリケーションをSailsアプリに移植する際には、Socket.ioを直接利用するのが有用かもしれません。Sailsはこのような用途に合わせて[socket.io](http://socket.io/)のサーバーインスタンス (`io`) へのアクセスを `sails.io`として提供しています。[Socket.ioドキュメンテーション](http://socket.io/docs/)に詳細があります。Socket.ioを直接利用する場合にはよく注意してください。

> v0.11.4のSailsではコアhook、[sails-hook-sockets](github.com/balderdashy/sails-hook-sockets)として`socket.io@v1.4.3`をbundleしています。





### 新しいapplicationオブジェクトを生成する (上級者向け)

複数のSails applicationインスタンスが必要になるような特殊な実装（例えば、Sails core向けのテストを書くなど）が必要な場合には、`require('sails')`で返されたインスタンスは_利用しない_でください。想定外の挙動をする場合があります。
代わりにSailsコンストラクタを利用して、applicationインスタンスを取得する必要があります。

```javascript
var Sails = require('sails').constructor;
var sails0 = new Sails();
var sails1 = new Sails();
var sails2 = new Sails();
```

それぞれのappインスタンス (`sails0`, `sails1`, `sails2`) は異なる設定の下、個別にロードまたはliftが可能です。

Sails自体をプログラマブルに利用したい場合には[Sailsのプログラム的に利用する](http://sailsjs-jp.org/documentation/concepts/programmatic-usage)を参照してください。


<docmeta name="displayName" value="Application">
