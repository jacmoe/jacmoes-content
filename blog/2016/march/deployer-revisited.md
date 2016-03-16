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

```
<?php
/* (c) Jacob Moen <jacmoe.dk@gmail.com>
*
* For the full copyright and license information, please view the LICENSE
* file that was distributed with this source code.
*/

require_once __DIR__ . '/common.php';

task('local-config', function () {

    if(askConfirmation("Local configuration.\n\nThis will overwrite any existing file without further warning!\n\nAre you sure you want to continue?")) {
        /**
        * Paser value for template compiler
        *
        * @param array $matches
        * @return string
        */
        $paser = function($matches) {
            if (isset($matches[1])) {
                if($matches[1] === 'release_path') {
                    $matches[1] = 'deploy_path';
                }
                $value = env()->get($matches[1]);
                if (is_null($value) || is_bool($value) || is_array($value)) {
                    $value = var_export($value, true);
                }
            } else {
                $value = $matches[0];
            }

            return $value;
        };

        /**
        * Template compiler
        *
        * @param string $contents
        * @return string
        */
        $compiler = function ($contents) use ($paser) {
            $contents = preg_replace_callback('/\{\{\s*([\w\.]+)\s*\}\}/', $paser, $contents);

            return $contents;
        };

        $finder   = new \Symfony\Component\Finder\Finder();
        $iterator = $finder
        ->ignoreDotFiles(false)
        ->files()
        ->name('/\.tpl$/')
        ->in(getcwd() . '/deployer/templates');

        $tmpDir = sys_get_temp_dir();
        $releaseDir = env('deploy_path');

        /* @var $file \Symfony\Component\Finder\SplFileInfo */
        foreach ($iterator as $file) {
            $success = false;
            // Make tmp file
            $tmpFile = tempnam($tmpDir, 'tmp');
            if (!empty($tmpFile)) {
                try {
                    $contents = $compiler($file->getContents());

                    // cookie validation key
                    if(basename($file) === 'web.php.tpl') {
                        $length = 32;
                        $bytes = openssl_random_pseudo_bytes($length);
                        $key = strtr(substr(base64_encode($bytes), 0, $length), '+/=', '_-.');
                        $contents = preg_replace('/(("|\')cookieValidationKey("|\')\s*=>\s*)(""|\'\')/', "\\1'$key'", $contents);
                    }

                    $target   = preg_replace('/\.tpl$/', '', $file->getRelativePathname());
                    // Put contents and upload tmp file to server
                    if (file_put_contents($tmpFile, $contents) > 0) {
                        if(basename($file) === 'yii.tpl') {
                            upload($tmpFile, "$releaseDir/" . $target);
                            run('chmod +x ' . "$releaseDir/" . $target);
                        } else {
                            run("mkdir -p $releaseDir/" . dirname($target));
                            upload($tmpFile, "$releaseDir/" . $target);
                        }
                        $success = true;
                    }
                } catch (\Exception $e) {
                    $success = false;
                }
                // Delete tmp file
                unlink($tmpFile);
            }
            if ($success) {
                writeln(sprintf("<info>✔</info> %s", $file->getRelativePathname()));
            } else {
                writeln(sprintf("<fg=red>✘</fg=red> %s", $file->getRelativePathname()));
            }
        }

    }
})->desc('Configures your local development environment')->onlyForStage('local');
```
lksdfj
