# Using MongoDB as a datastore in a Sails app

Sails supports the popular [MongoDB database](https://www.mongodb.com/) via the [`sails-mongo` adapter](https://www.npmjs.com/package/sails-mongo).

To use `sails-mongo` in your app:

1. Make sure you have access to a running MongoDB server, either on your development machine or in the cloud.
2. Run `npm install sails-mongo --save` in your app folder.
3. In your `config/datastores.js` file, edit the `default` datastore configuration:

    ```js
    default: {
      adapter: 'sails-mongo',
      url: <connection string for your mongo server, e.g. 'mongodb://localhost:27017/myMongoDb'>
    }
    ```
4. In your `config/models.js` file, add/edit the default `id` attribute to set the correct `type` and `columnName` for MongoDB primary keys:

    ```js
    attributes: {
      id: { type: 'string', columnName: '_id' }
    }
    ```
5. _Optional_: if you don&rsquo;t want a particular model to use a MongoDB ObjectID as its primary key, set the `dontUseObjectIds` flag to `true` in that model file, and set up its primary key attribute manually:

   ```js
   // api/models/User.js
   module.exports = {
     dontUseObjectIds: true,
     attributes: {
       id: { type: 'number', columnName: '_id' }, // <-- still need to set `columnName`!
       name: { type: 'string' },
       ...etc...
     }
   }
   ```

As with all of the [Sails database adapters](http://sailsjs.com/documentation/concepts/extending-sails/adapters/available-adapters), you can use any of the [Waterline model methods](http://sailsjs.com/documentation/reference/waterline-orm/models) to interact with your models when using `sails-mongo`.  You can also access the lower-level &ldquo;native&rdquo; MongoDB client to send more complex queries, using the [`.manager()` method](http://sailsjs.com/documentation/reference/waterline-orm/datastores/manager) of the [datastore instance](http://sailsjs.com/documentation/reference/application/sails-get-datastore):

```js
// Get access to the native MongoDB client via the default Sails datastore.
var db = sails.getDatastore().manager;

// Find all users who own albums with the word "blue" in the title.
// ("albums" would be defined in `api/models/User.js` as an attribute of type "json".)
db.collection('user').find({"albums.title": {"$regex": /blue/}}).toArray(console.log);
```

For a full list of methods available in the native MongoDB client, see the <a href="http://mongodb.github.io/node-mongodb-native/2.2/api/Collection.html" target="_blank">Node.js MongoDB Driver API reference</a>.


<docmeta name="displayName" value="Using MongoDB">
