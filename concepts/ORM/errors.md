# Errors

When a call to any model method fails, `err` is returned. This `err` is a [JavaScript Error instance](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error) whose properties can be useful in diagnosing what went wrong.
```usage
Something.create()
.exec(function(err) {...});
```
Waterline normalizes these Error instances, classifying them with consistent `err.name` values and, when applicable, `err.code`.

> The only time a Waterline model method might not return a normalized Error instance is in the case of a synchronous method such as [.validate()](http://sailsjs.com/documentation/reference/waterline-orm/models/validate). When a synchronous method fails, it will throw, since it has no callback.


### Negotiating errors

Catchall error handling, while better than nothing, often just isn't enough. (There's a big difference between "that is not a valid username" and "we aren't able to create new users at all right now".) In order to negotiate the different kinds of errors appropriately, you'll need to be able to examine them in a granular way.


| Property       | Type          | Details            |
|:---------------|---------------|:-------------------|
| name           | ((string))    | The broad classification of the error. <br/><br/> e.g.`'UsageError'`     |
| message        | ((string))    | <em>See [.message](https://nodejs.org/dist/latest-v7.x/docs/api/errors.html#errors_error_message).</em> |
| stack          | ((string))    | <em>See [.stack](https://nodejs.org/dist/latest-v7.x/docs/api/errors.html#errors_error_stack).<em>     |
| _code_         | ((string?))   | A narrower classification of the error that is sometimes included.<br/><br/>e.g. `'E_UNIQUE'`       |

When using code that interacts with Waterline (usually through model methods) there are a few different kinds of error you may encounter.


### Usage errors

When an error has `name: 'UsageError'`, this indicates that a Waterline method was used incorrectly, or executed with invalid options (for example, attempting to create a new record that would violate one of your model's [high-level validation rules](http://sailsjs.com/documentation/concepts/models-and-orm/validations#?validation-rules).)

This sort of error can come from any model method.

```
err.name === 'UsageError'
```

### Adapter errors

Adapter errors usually indicate a problem in the underlying adapter, and not in the request itself. This can happen when a database goes offline, when there is a permission issue, because of some database-specific edge case, or (more rarely) a bug in the adapter. This kind of error will have `name: 'AdapterError'`.

This sort of error can come from any model method.

```
err.name === 'AdapterError'
```


##### E_UNIQUE

A uniqueness error occurs when a value that _should_ be unique matches that of another record in the database. While this is considered an adapter error, it has its own `code` to differentiate it from a normal adapter error: `code: 'E_UNIQUE'`.

This sort of error can only come from the `.create()`, `.update()`, `.addToCollection()`, and `.replaceCollection()` model methods.

```
err.code === 'E_UNIQUE'
```

### Example

The exact strategy you use to do this in your Sails app depends on whether you're using [callbacks or promises](https://github.com/balderdashy/sails/issues/3459#issuecomment-171039631).  Remember: use whatever you're most comfortable with.  If you aren't sure, start with callbacks.

##### Negotiating errors with callbacks

To handle the different errors that may occur when attempting to create a new user:

```javascript
User.create({
  email: req.param('email')
})
.exec(function(err){
  if (err){
    // Uniqueness constraint violation
    if (err.code === 'E_UNIQUE') {
      return res.status(409).json(err);
    }
    // Some other kind of usage / validation error
    else if (err.name === 'UsageError') {
      return res.badRequest(err);
    }
    // If something completely unexpected happened.
    else {
      return res.serverError(err);
    }
  }

  return res.ok();
})
```

##### Negotiating errors with promises

To handle the different errors that may occur when attempting to create a new user:

```javascript
User.create({
  email: req.param('email')
})
.then(function (){
  return res.ok();
})
// Uniqueness constraint violation
.catch({ code: 'E_UNIQUE' }, function (err) {
  return res.status(401).json(err);
})
// Some other kind of usage / validation error
.catch({ name: 'UsageError' }, function (err) {
  return res.badRequest(err);
})
// If something completely unexpected happened.
.catch(function (err) {
  return res.serverError(err);
});
```


<docmeta name="displayName" value="Errors">
