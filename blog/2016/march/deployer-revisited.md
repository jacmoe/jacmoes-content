<!--
Title: Deployer revisited
Author: Jacob Moen
Date: 2016/03/17 20:02
Datetime: 2016-03-17
Description: Deployer now handles all configuration of my Yii projects
View: post
Disqusid: /2016/march/deployer-revisited
ogimage: deployer2/localconfig.png
thumb: deployer2/localconfig_custom.png
Keywords: deployer, yii, configuration, deployment
Tags: yii, deployer, deployment
blogpost: true
published: true
-->
(lightbox:Deployer local config source:deployer2/localconfig_mobile.png target:deployer2/localconfig.png)
In a [[blog/2016/january/deploying-yii-with-deployer|previous]] blog post I wrote about using the excellent deployment tool [Deployer](http://deployer.org/) with [Yii](http://www.yiiframework.com/), and I now use it every web project I work on.

All my projects are deployed using the simple `dep deploy` command and I am happy with it as it is a flexible and seamless process.

(clearfix:)


## Master configuration file

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
And, a relevant section of the `config/web.php.tpl` configuration template:

```php
'reCaptcha' => [
    'name' => 'reCaptcha',
    'class' => 'himiklab\yii2\recaptcha\ReCaptcha',
    'siteKey' => '{{app.recaptcha.siteKey}}',
    'secret' => '{{app.recaptcha.secret}}',
```

These templates are processed as part of the deployment process, using a custom recipe `yii-configure` - see [yii2-app-basic-deployer](https://github.com/jacmoe/yii2-app-basic-deployer) - in the `deployer/recipes` directory.

## Transpilation
(inimage: Transpilation system source:deployer2/transpile.png align:right)
The idea is to edit the configuration templates instead of touching `config/web.php` and `config/console.php` - in fact, they are added to my `.gitignore` and that all variables are kept safely in one file only, the `servers.yml` file. Obviously, that file is also not committed to source control.

Now, when adding to the configuration, I edit the templates and issue a `dep local-config local` command and the scripts are updated.

I find it to be safer and less error-prone than having to juggle two (or more) sets of configuration files.

And the chances of forgetting to update the other when one changes are eliminated. And there is only one file to worry about: the `servers.yml` master configuration file.

That one could be stored in a secure vault for safe-keeping.

(clearfix:)
## Local config script
Obviously, this is only going to be useful if you are able to transpile the templates *"in-place"* when developing.

And that is why I have hacked together a local version of that script, cleverly entitled *local-config* that does just that: run the templates through a template parser and put the processed files where they are supposed to be.

And then, generating them is just a simple Deployer command/task:

```
dep local-config local
```

Since the task will overwrite any existing files, I have gotten into the good habit of treating the generated files as read-only output and only edit/tweak the templates.

In my experience, there are much less room for errors that way.

The recipe is to be found in the aforementioned yii2-app-basic-deployer repository: [local-config.php](https://github.com/jacmoe/yii2-app-basic-deployer/blob/master/deployer/recipe/local-config.php).

I hope it proves to be as useful to you as it is for me.

**Note** that this recipe is the local version of the `yii-configure` recipe that is used for *real* deployment.  
That is: both recipes are needed.
