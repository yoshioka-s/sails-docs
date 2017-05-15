# Locals

The variables accessible in a particular view are called `locals`.  Locals represent server-side data that is _accessible_ to your view-- locals are not actually _included_ in the compiled HTML unless you explicitly reference them using special syntax provided by your view engine.

```ejs
<div>Logged in as <a><%= name %></a>.</div>
```

### Using locals in your views

The notation for accessing locals varies between view engines.  In EJS, you use special template markup (e.g. `<%= someValue %>`) to include locals in your views.

There are three kinds of template tags in EJS:
+ `<%= someValue %>`
  + HTML-escapes the `someValue` local, and then includes it as a string.
+ `<%- someRawHTML %>`
  + Includes the `someRawHTML` local verbatim, without escaping it.
  + Be careful!  This tag can make you vulnerable to XSS attacks if you don't know what you're doing.
+ `<% if (!loggedIn) { %>  <a>Logout</a>  <% } %>`
  + Runs the JavaScript inside the `<% ... %>` when the view is compiled.
  + Useful for conditionals (`if`/`else`), and looping over data (`for`/`each`).


Here's an example of a view (`views/backOffice/profile.ejs`) using two locals, `user` and `corndogs`:

```ejs
<div>
  <h1><%= user.name %>'s first view</h1>
  <h2>My corndog collection:</h2>
  <ul>
    <% _.each(corndogs, function (corndog) { %>
    <li><%= corndog.name %></li>
    <% }) %>
  </ul>
</div>
```

> You might have noticed another local, `_`.  By default, Sails passes down a few locals to your views automatically, including lodash (`_`).

If the data you wanted to pass down to this view was completely static, you don't necessarily need a controller- you could just hard-code the view and its locals in your `config/routes.js` file, i.e:

```javascript
  // ...
  'get /profile': {
    view: 'backOffice/profile',
    locals: {
      user: {
        name: 'Frank',
        emailAddress: 'frank@enfurter.com'
      },
      corndogs: [
        { name: 'beef corndog' },
        { name: 'chicken corndog' },
        { name: 'soy corndog' }
      ]
    }
  },
  // ...
```

On the other hand, in the more likely scenario that this data is dynamic, we'd need to use a controller action to load it from our models, then pass it to the view using the [res.view()](http://sailsjs.com/documentation/reference/res/res.view.html) method.

Assuming we hooked up our route to one of our controller's actions (and our models were set up), we might send down our view like this:

```javascript
// in api/controllers/UserController.js...

  profile: function (req, res) {
    // ...
    return res.view('backOffice/profile', {
      user: theUser,
      corndogs: theUser.corndogCollection
    });
  },
  // ...
```

### Escaping untrusted data using `exposeLocalsToBrowser`

It is often desirable to &ldquo;bootstrap&rdquo; data onto a page so that it&rsquo;s available via Javascript as soon as the page loads, instead of having to fetch the data in a separate AJAX or socket request.  Sites like [Twitter and GitHub](https://blog.twitter.com/2012/improving-performance-on-twittercom) rely heavily on this approach in order to optimize page load times and provide an improved user experience.

In the past, a common way of solving this problem was with hidden form fields, or by hand-rolling code that injects server-side locals directly into a client-side script tag.  However, these techniques can present a challenge when some of the data you want to bootstrap is from an _untrusted_ source, meaning that it might contain HTML tags and Javascript code meant to compromise your app with an <a href="https://en.wikipedia.org/wiki/Cross-site_scripting" target="_blank">XSS attack</a>.  To help prevent such issues, Sails provides a helper function called `exposeLocalsToBrowser` that you can use in your views to output data safely.

To use `exposeLocalsToBrowser`, simply call it from within your view using the _non-escaping syntax_ for your template language.  For example, using the default EJS view engine, you would do:

```ejs
<%- exposeLocalsToBrowser() %>
```

By default, this exposes _all_ of your view locals as the `window.SAILS_LOCALS` global variable.  For example, if your action code contained:

```javascript
res.view('myView', {
  someString: 'hello',
  someNumber: 123,
  someObject: { owl: 'hoot' },
  someArray: [1, 'boot', true],
  someBool: false
  someXSS: '<script>alert("all your credit cards is belongs to us");</script>'
});
```

then using `exposeLocalsToBrowser` as shown above would cause the locals to be safely bootstrapped in such a way that `window.SAILS_LOCALS.someArray` would contain the array `[1, 'boot', true]`, and  `window.SAILS_LOCALS.someXSS` would contain the _string_ `<script>alert("all your credit cards is belongs to us");</script>`, without causing that code to actually be executed on the page.

The `exposeLocalsToBrowser` function has a single `options` parameter that can be used to configure what data is outputted, and how.  The `options` parameter is a dictionary that can contain the following properties:

|&nbsp;   |     Property        | Type                                         | Default| Details                            |
|---|:--------------------|----------------------------------------------|:-----------------------------------|-----|
| 1 | _keys_     | ((array?))                              | `undefined` | A &ldquo;whitelist&rdquo; of locals to expose.  If left undefined, _all_ locals will be exposed.  If specified, this should be an array of property names from the locals dictionary.  For example, given the `res.view()` statement shown above, setting `keys: ['someString', 'someBool']` would cause `windows.SAILS_LOCALS` to be set to `{someString: 'hello', someBool: false}`.
| 2 | _namespace_ | ((string?)) | `SAILS_LOCALS` | The name of the global variable to assign the bootstrapped data to.
| 3| _dontUnescapeOnClient_ | ((boolean?)) | false | **Advanced. Not recommended for most apps.** If set to `true`, any string values that were escaped to avoid XSS attacks will _still be escaped_ when accessed from client-side JS, instead of being transformed back into the original value.  For example, given the `res.view()` statement from the example above, using `exposeLocalsToBrowser({dontUnescapeOnClient: true})` would cause `window.SAILS_LOCALS.someXSS` to be set to `&lt;script&gt;alert(&#39;hello!&#39;);`.


<docmeta name="displayName" value="Locals">
