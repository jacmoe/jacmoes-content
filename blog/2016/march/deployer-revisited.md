<!--
Title: Deployer revisited
Author: Jacob Moen
Date: 2016/03/16 20:02
Datetime: 2016-03-16
Description: Deployer now handles all configuration of my Yii projects
View: post
Disqusid: /2016/march/deployer-revisited
ogimage: deployer2/localconfig.png
thumb: deployer2/localconfig_custom.png
Keywords: deployer, yii, configuration, deployment
Tags: yii, deployer, deployment
blogpost: true
published: false
-->
(lightbox:Deployer local config source:deployer2/localconfig_mobile.png target:deployer2/localconfig.png)
In a [[blog/2016/january/deploying-yii-with-deployer|previous]] blog post I wrote about using the excellent deployment tool [Deployer](http://deployer.org/) with [Yii](http://www.yiiframework.com/), and I have found myself using it on a daily basis ever since.

All my projects are deployed using the simple `dep deploy` command and I am happy with it as it is a flexible and seamless process.

(clearfix:)

I am a big fan of the idea of having a master configuration file for both local and remote servers (environments), but I am also a big fan of developing "in-place", i.e. serving the development site directly from the source directory instead of maintaining a separate dev deployment directory.

In my previous article about using Deployer with Yii I described how I am using a custom recipe to transpile server variables into template files.

Not only Deployer specific variables, like `host`, `user`, `repository` and `deploy_path`, but also application specific *secrets* like this:

```yaml
recaptcha:
    siteKey: 'sadfsadfasfawerfawefawefeaw'
    secret: 'awefawefawefewarwearwaecfwae'

auth:
    twitter:
        consumerKey: 'afewafaewrewrwaegerge'
        consumerSecret: 'eagwergergratawrtaretret'

    google:
        clientId: 'ewfweafwaefweafwaefwaefwe'
        clientSecret: 'wafeawfwearewrwerrwt'
```
And, the `web.php.tpl` configuration template:

```php
'reCaptcha' => [
    'name' => 'reCaptcha',
    'class' => 'himiklab\yii2\recaptcha\ReCaptcha',
    'siteKey' => '{{app.recaptcha.siteKey}}',
    'secret' => '{{app.recaptcha.secret}}',
```
These templates are processed as part of the deployment process, using a custom recipe `yii-configure` - see [yii2-app-basic-deployer](https://github.com/jacmoe/yii2-app-basic-deployer) - in the `deployer/recipes` directory.

But wouldn't it be nice to be able to transpile the templates in development mode as well, like *"in-place"* ?

Yes, that is why I have hacked together a local version of that script, cleverly entitled *local-config* that does just that: run the templates through a template parser - because, how else would I be able to configure the development environment properly if I didn't? :)

The idea is to edit the configuration templates instead of touching `config/web.php` and `config/console.php` - in fact, they are added to my `.gitignore` and that all variables are kept safely in one file only, the `servers.yml` file. Obviously, that file is also not committed to source control.

(inimage: Transpilation system source:deployer2/transpile.png align:right)