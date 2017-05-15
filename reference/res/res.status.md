# res.status()

Set the status code of this response.

### Usage
```usage
res.status(200);
```

### Example
```javascript
res.status(404);
res.send('oops');
```

### Notes
>+ The status code may be set up until the response is sent.
>+ `res.status()` is effectively just a chainable alias of node's '`res.statusCode=`.










<docmeta name="displayName" value="res.status()">
<docmeta name="pageType" value="method">
