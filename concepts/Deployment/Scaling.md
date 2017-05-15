# Scaling

If you have the immediate expectation of lots of traffic to your application (or better yet, you already have the traffic),
you'll want to set up a scalable architecture that will allow you to add servers as more and more requests hit your app.

### Performance

In production, Sails performs like any Connect, Express or Socket.io app ([example](http://serdardogruyol.com/?p=111)).  If you have your own benchmark you'd like to share, please write a blog post or article and tweet [@sailsjs](http://twitter.com/sailsjs).  But benchmarks aside, keep in mind that most performance and scalability metrics are application-specific.  The actual performance of your app will have a lot more to do with the way you implement your business logic and model calls than it will about the underlying framework you are using.



### Example architecture

```
                             ....
                    /  Sails.js server  \      /  Database (e.g. Mongo, Postgres, etc)
Load Balancer  <-->    Sails.js server    <-->    Socket.io message queue (Redis)
                    \  Sails.js server  /      \  Session store (Redis, Mongo, etc.)
                             ....
```


### Preparing your app for a clustered deployment

Node.js (and consequently Sails.js) apps scale horizontally. It's a powerful, efficient approach, but it involves a tiny bit of planning. At scale, you'll want to be able to copy your app onto multiple Sails.js servers and throw them behind a load balancer.

One of the big challenges of scaling an application is that these sorts of clustered deployments cannot share memory, since they are on physically different machines. On top of that, there is no guarantee that a user will "stick" with the same server between requests (whether HTTP or sockets), since the load balancer will route each request to the Sails server with the most available resources. The most important thing to remember about scaling a server-side application is that it should be **stateless**.  That means you should be able to deploy the same code to _n_ different servers, expecting any given incoming request handled by any given server, and everything should still work.  Luckily, Sails apps come ready for this kind of deployment almost right out of the box.  But before deploying your app to multiple servers, there are a few things you need to do:

+ Ensure none of the other dependencies you might be using in your app rely on shared memory.
+ Make sure the database(s) for your models (e.g. MySQL, Postgres, Mongo) are scalable (e.g. sharding/cluster)
+ **If your app uses sessions:**
  + Configure your app to use a shared session store such as Redis (simply uncomment the `adapter` option in `config/session.js`) and install the connect-redis adapter as a dependency of your app (e.g. `npm install connect-redis@~3.0.2 --save --save-exact`). For more information about configuring your session store for production, see the [sails.config.session](http://sailsjs.com/documentation/reference/configuration/sails-config-session#?production-config) docs.
+ **If your app uses sockets:**
  + Configure your app to use Redis as a shared message queue for delivering socket.io messages. Socket.io (and consequently Sails.js) apps support Redis for sockets by default, so to enable a remote redis pubsub server, uncomment the relevant lines in `config/env/production.js`.
  + Install the socket.io-redis adapter as a dependency of your app (e.g. `npm install socket.io-redis@^3.0.0 --save --save-exact`)
+ **If your cluster is on a single server (for instance, using [pm2 cluster mode](http://pm2.keymetrics.io/docs/usage/cluster-mode/))**
  + To avoid file conflict issues due to Grunt tasks, always start your apps in `production` environment, and/or consider [turning Grunt off completely](http://sailsjs.com/documentation/concepts/assets/disabling-grunt).  See [here](https://github.com/balderdashy/sails/issues/3577#issuecomment-184786535) for more details on Grunt issues in single-server clusters
  + Be careful with [`config/bootstrap.js` code](http://sailsjs.com/documentation/reference/configuration/sails-config-bootstrap) that persists data in a database, to avoid conflicts when the bootstrap runs multiple times (once per node in the cluster)

### Deploying a Node/Sails app to a PaaS

Deploying your app to a PaaS like Heroku or Modulus is dead simple. Depending on your situation, there may still be a few devils in the details, but Node support with hosting providers has gotten _really good_ over the last couple of years.  Take a look at [Hosting](http://sailsjs.com/documentation/concepts/deployment/Hosting) for more platform-specific information.

### Deploying your own cluster

+ Deploy multiple instances (aka servers running a copy of your app) behind a [load balancer](https://en.wikipedia.org/wiki/Load_balancing_(computing)) (e.g. nginx)
  + Configure your load balancer to terminate SSL requests
  + But remember that you won't need to use the SSL configuration in Sails-- the traffic will already be decrypted by the time it reaches Sails.
  + Lift your app on each instance using a daemon like `forever` or `pm2` (see http://sailsjs.com/documentation/concepts/deployment for more about daemonology)


### Optimization

Optimizing an endpoint in your Node/Sails app is exactly like optimizing an endpoint in any other server-side application; e.g. identifying and manually optimizing slow queries, reducing the number of queries, etc.  Specifically for Node apps, if you find you have a heavily trafficked endpoint that is eating up CPU, look for synchronous (blocking) model methods, services, or machines that might be getting called over and over again in a loop or recursive dive.

But remember:

> Premature optimization is the root of all evil.  -[Donald Knuth](http://c2.com/cgi/wiki?PrematureOptimization)

No matter what tool you're using, it is important to spend your focus and time on writing high quality, well documented, readable code.  That way, if/when you are forced to optimize a code path in your application, you'll find it is much easier to do so.



### Notes

> + You don't have to use Redis for your sessions-- you can actually use any Connect or Express-compatible session store.  See [sails.config.session](sailsjs.com/documentation/reference/configuration/sails-config-session) for more information.
> + Some hosted Redis providers (such as <a href="https://elements.heroku.com/addons/redistogo" target="_blank">Redis To Go</a>) set a <a href="https://redis.io/topics/clients#client-timeouts" target="_blank">timeout for idle connections</a>.  In most cases you&rsquo;ll want to turn this off to avoid unexpected behavior in your app.  Details on how to turn off the timoeout vary depending on provider (you may have to contact their support team).

<docmeta name="displayName" value="Scaling">
