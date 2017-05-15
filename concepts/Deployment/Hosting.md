# Hosting

Here is a non-comprehensive list of Node/Sails hosting providers and a few available community tutorials.  Keep in mind that, most of the time, the process for deploying your Sails app is exactly the same as it would be for any other Node.js app.  Just be sure to take a look at the [other pages](http://sailsjs.com/documentation/concepts/deployment) in this section of the docs (as well as your app's [`config/env/production.js` file](http://sailsjs.com/documentation/anatomy/config/env/production-js)) and make any necessary adjustments before you actually deploy to production.


### Heroku

<a title="Deploy your Sails/Node.js app on Heroku" href="http://heroku.com"><img style="width:285px;" src="http://sailsjs.com/images/deployment_heroku.png" alt="Heroku logo"/></a>

+ [Hello Sails.js: Hosting your Sails.js application on Heroku](https://hellosails.com/hosting-your-sails-js-application-heroku/)
+ [Platzi: Develop Apps with Sails.js: Pt 2](https://courses.platzi.com/classes/develop-apps-sails-js/)  _(see part 2)_
+ [SailsCasts: Deploying a Sails App to Heroku](http://irlnathan.github.io/sailscasts/blog/2013/11/05/building-a-sails-application-ep26-deploying-a-sails-app-to-heroku/)
+ [Sails.js on Heroku](http://vort3x.me/sailsjs-heroku/)
+ https://groups.google.com/forum/#!topic/sailsjs/vgqJFr7maSY
+ https://github.com/chadn/heroku-sails
+ http://dennisrongo.com/deploying-sails-js-to-heroku
+ http://stackoverflow.com/a/20184907/486547

### Microsoft Azure

<a title="Deploy a Sails.js web app to Azure App Service" href="https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-nodejs-sails"><img style="width:350px;" src="http://sailsjs.com/images/deployment_azure.png" alt="Azure logo"/></a>

+ [Deploy a Sails.js web app to Azure App Service](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-nodejs-sails)
+ [Deploying Sails.js to Azure Web Apps](https://blogs.msdn.microsoft.com/partnercatalystteam/2015/07/16/y-combinator-collaboration-deploying-sailsjs-to-azure-web-apps/)

### Google Cloud Platform

<a title="Deploy your Sails/Node.js app to Google Cloud Platform" href="https://cloud.google.com/nodejs/resources/frameworks/sails"><img style="width:350px;" src="http://sailsjs.com/images/deployment_googlecloud.png" alt="Google Cloud Platform logo"/></a>

> It's easy to get enterprise-grade Sails.js apps running on Google Cloud Platform. And because the apps you create will be running on the same infrastructure that powers all of Google's products, you can be confident that they will scale to serve all of your users, whether there are a few or millions of them.

+ [Run Sails.js on Google Cloud Platform](https://cloud.google.com/nodejs/resources/frameworks/sails)
+ [Deploying Sails.js to Google Cloud](http://www.mot.la/2016-06-04-deploying-sails-js-to-google-cloud.html)
+ [A couple of Googlers demonstrate and deploy their app built on Sails.js and GO in a talk called `runtime:yours` at Google Cloud Platform Live](https://www.facebook.com/sailsjs/posts/721341477911963)


### DigitalOcean

<a title="DigitalOcean" href="https://aws.amazon.com/"><img style="width:225px;" src="http://sailsjs.com/images/deployment_digitalocean.png" alt="DigitalOcean logo"/></a>

+ [Troubleshooting: Can't install Sails.js on DigitalOcean](https://www.digitalocean.com/community/questions/can-t-install-sails-js)
+ [How to create a Node.js app using Sails.js on an Ubuntu VBS](https://www.digitalocean.com/community/articles/how-to-create-an-node-js-app-using-sails-js-on-an-ubuntu-vps)
+ https://www.digitalocean.com/community/articles/how-to-use-pm2-to-setup-a-node-js-production-environment-on-an-ubuntu-vps
+ https://www.digitalocean.com/community/articles/how-to-host-multiple-node-js-applications-on-a-single-vps-with-nginx-forever-and-crontab


### Amazon Web Services (AWS)

<a title="Amazon Web Services (AWS)" href="https://aws.amazon.com/"><img style="width:275px;" src="http://sailsjs.com/images/deployment_aws.png" alt="AWS logo"/></a>


+ [Creating a Sails.js application on AWS](http://bussing-dharaharsh.blogspot.com/2013/08/creating-sailsjs-application-on-aws-ami.html) _(see also [this question on ServerFault](http://serverfault.com/questions/531560/creating-an-sails-js-application-on-aws-ami-instance))_
+ [Deploying Sails/Node.js apps to AWS](http://cloud.dzone.com/articles/how-deploy-nodejs-apps-aws-mac)
+ [Deploy a Sails app to AWS](https://www.distelli.com/docs/tutorials/build-and-deploy-sails-angular-application)
+ [Your own mini-Heroku on AWS](http://blog.grio.com/2014/01/your-own-mini-heroku-on-aws.html)


### PM2 (KeyMetrics)

<a title="About PM2" href="http://pm2.keymetrics.io/"><img style="width:285px;" src="http://sailsjs.com/images/deployment_pm2.png" alt="PM2 logo"/></a>

+ [Deploying with PM2](http://devo.ps/blog/goodbye-node-forever-hello-pm2/)

> Note: PM2 isn't really a hosting platform, but it's worth mentioning in this section just so you're aware of it.


### OpenShift (Red Hat)

<a href="https://www.openshift.com/"><img style="width:350px;" alt="Red Hat™ OpenShift logo" src="http://sailsjs.com/images/deployment_openshift.png"/></a>

+ [Deploying a Sails / Node.js application to OpenShift](https://gist.github.com/mikermcneil/b6136aa219f6d15b01a05b14cc681fcb)
+ [Listening to a different IP address on OpenShift](https://coderwall.com/p/dhhfcw/sailsjs-listening-on-a-different-ip-address) _(courtesy [@otupman](https://github.com/otupman))_
+ [Get Sails/Node.js running on OpenShift](https://gist.github.com/mdunisch/4a56bdf972c2f708ccc6) _(Warning: quite out of date, but still useful for context.  Courtesy [@mdunisch](https://github.com/mdunisch).)_


### Xervo (formerly Modulus)

<a href="https://xervo.io"><img alt="Xervo logo" style="display: inline-block; width: 85px;" src="http://sailsjs.com/images/deployment_xervo.png"/>&nbsp; &nbsp;<img alt="Modulus logo" style="display: inline-block; width: 85px;" src="http://sailsjs.com/images/deployment_modulus.png"/></a>

+ [Customer Spotlight: Sails.js](https://blog.xervo.io/sails-js)


### exoscale / CloudControl

+ [Deploying a Sails.js application to exoscale / CloudControl](https://github.com/exoscale/apps-documentation/blob/88d9f157093f0690f139337ff934c027482d4727/Guides/NodeJS/Sailsjs.md) _([rendered version of tutorial](https://webcache.googleusercontent.com/search?q=cache:gq8UZXarNq8J:https://community.exoscale.ch/documentation/apps/nodejs-app-sailsjs/+&cd=1&hl=en&ct=clnk&gl=us))_


### RoseHosting

 + [Install Sails.js with Apache as a reverse proxy on CentOS 7](https://www.rosehosting.com/blog/install-sails-js-with-apache-as-a-reverse-proxy-on-centos-7/)
 + [Install Sails.js on Ubuntu](https://www.rosehosting.com/blog/install-the-sails-js-framework-on-an-ubuntu-vps/)
 + All hosting plans from RoseHosting are fully-managed with free 24/7 support, so you can contact their [support team](https://www.rosehosting.com/support.html) and they will install and configure Sails.js for you for free




<docmeta name="displayName" value="Hosting">
