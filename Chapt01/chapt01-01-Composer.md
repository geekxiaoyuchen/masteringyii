# Composer
There are several different ways to install Yii2, ranging from downloading the framework from source control (typically, from GitHub at https://github.com/yiisoft/yii2) to using a package manager such as Composer. With modern web applications, Composer is the preferred method to install Yii2 as it enables us to install, update, and manage all dependencies and extensions for our application in an automated fashion. Additionally, using Composer, we can ensure that Yii Framework 2 is kept up to date with the latest security and bug xes. Composer can be installed by following the instructions on https://getcomposer.org. Typically, this process looks as follows:

有多种不同方法安装Yii2，包括从版本控制工具下载安装包（通常，使用[GitHub](https://github.com/ yiisoft/yii2)，或者使用包管理工具，比如Composer。Composer可以帮助我们自动化安装、更新、管理依赖与扩展，因此，从现代Web应用的角度说，推荐使用Composer来安装Yii2。此外，通过Composer，我们可以确保Yii2能够及时更新最新版和Bug修正。可以通过以下的命令来安装[Composer](https://getcomposer.org)


     curl -sS https://getcomposer.org/installer | php
Alternatively, if you don't have cURL available on your system, it can be installed through PHP itself:
如何你没有安装cURL，你也可以使用PHP来安装Composer，命令如下：

    php -r "readfile('https://getcomposer.org/installer');" | ph
Once installed, we should move Composer to a more centralized directory so that we can call it from any directory on our system. Installing Composer from a centralized directory rather than on a per-project basis has several advantages:

安装完成之后，你应该将Composer移动到主目录，以便我们可以在任何文件夹下使用它。因为这么做可以获取以下几点好处：

*   It can be called anywhere from any project. When working with multiple projects, we can ensure that we use the same dependency manager each time and for every project.

*   任何项目均可调用。当在多个项目工作时，我们可以确保使用同样的依赖管理。

*   In a centralized directory, Composer only needs to be updated once rather than in every project we are working on.

* 安装在主目录，Composer只需要更新一次而不需要在每个项目目录里更新。

*   Dependency managers are rarely considered code that should be pushed to your DCVS repository. Keeping the composer.phar file out of your repository reduces the amount of code you need to commit and push and ensures that your source code remains isolated from your package manager code.

* 依赖管理很少需要被当作需要提交到版本仓库的代码。只需要将Composer.phar排除在代码仓库之外，确保我的代码独立于包管理代码。

*   By installing Composer from a centralized directory, we can ensure that Composer is always available, which saves us a step each time we clone a project that depends on Composer.

* 将Composer安装在主目录，我们可以保证Composer总是可以被使用，这样可以节省每次克隆依赖于Composer项目的时间。

A good directory to move Composer to is /usr/local/bin, as shown in the following example:
可以通过以下命令将Composer移动到/usr/local/bin主目录。

    mv composer.phar /usr/local/bin/composer
    chmod a+x /usr/local/bin/composer
Alternatively, if you have Composer installed on your system already, ensure that you update it to the latest version by running this:
此外，如果你已经安装Composer，可以通过下面这条命令保持Composer更新到最新版本。

    composer self-update
Once Composer is installed, we'll need to install a global plugin called The Composer Asset Plugin (available at https://github.com/francoispluchino/ composer-asset-plugin). This plugin enables Composer to manage asset les for us without the need to install additional software (these programs are Bower, an asset dependency manager created by Twitter, and Node Package Manager, or NPM, which is a JavaScript dependency manager).

Composer安装之后，我们需要安装一个叫[Composer Asset Plugin](https://github.com/francoispluchino/)的全局插件。这个插件帮助我们自动下载管理资源，而不用每个都下载安装（比如Bower，一个Twitter创建的资源依赖管理，NPM，一个Javascript依赖管理）

    composer global require "fxp/composer-asset-plugin:1.0.0"
With Composer installed, we can now instantiate our application. If we want to install an existing Yii2 package, we can simply run the following:

Composer安装后，我们现在可以创建就应用。如果我们想安装Yii2包，只需要简单运行如下命令：

    composer create-project --prefer-dist <package/name> <foldername> 
Using the Yii2 basic app as an example, this command will look like this:
例如我们想安装Yii基础应用，可以输入以下命令：

    composer create-project --prefer-dist yiisoft/yii2-app-basic basic 
After running the command, you should see output similar to the following:
输入命令后，我们应该会得到下面的输出：

```
Installing yiisoft/yii2-app-basic (2.0.6)
  - Installing yiisoft/yii2-app-basic (2.0.6) 

Downloading: 100%
Created project in basic
Loading composer repositories with package information
Installing dependencies (including require-dev)
- Installing yiisoft/yii2-composer (2.0.3)
  - Installing ezyang/htmlpurifier (v4.6.0)
  - Installing bower-asset/jquery (2.1.4)
  - Installing bower-asset/yii2-pjax (v2.0.4)
  - Installing bower-asset/punycode (v1.3.2)
  - Installing bower-asset/jquery.inputmask (3.1.63)
  - Installing cebe/markdown (1.1.0) 

 - Installing yiisoft/yii2 (2.0.6)
  - Installing swiftmailer/swiftmailer (v5.4.1)
  - Installing yiisoft/yii2-swiftmailer (2.0.4)
  - Installing yiisoft/yii2-codeception (2.0.4)
  - Installing bower-asset/bootstrap (v3.3.5)
  - Installing yiisoft/yii2-bootstrap (2.0.5)
  - Installing yiisoft/yii2-debug (2.0.5)
  - Installing bower-asset/typeahead.js (v0.10.5)
  - Installing phpspec/php-diff (v1.0.2)
  - Installing yiisoft/yii2-gii (2.0.4)
  - Installing fzaninotto/faker (v1.5.0)
  - Installing yiisoft/yii2-faker (2.0.3) 

Writing lock file
Generating autoload files
> yii\composer\Installer::postCreateProject
chmod('runtime', 0777)...done.
chmod('web/assets', 0777)...done.
chmod('yii', 0755)...done.
```
This command will install the Yii2 basic app to a folder called basic. When creating a new Yii2 project, you'll typically want to use the create-project command to clone "yii2-app-basic" and then develop your application from there as the basic app comes prepopulated with just about everything you need to start a new project. However, you can also create a Yii2 project from scratch that, while more complicated, gives you more control over your application's structure.

这行命令会在basic文件夹下安装Yii基础应用。创建Yii2项目时，经常会使用create-porject命令来克隆"yii2-app-basic"，在这个基础应用的基础上可以快速的开发自己的应用。当然，你也可以使用该命令创建更为复杂的Yii2应用，这样你可以更好的控制应用结构。

Let's take a look at the composer.json le that was created when we ran the create-project command:
让我们看一下执行create-project命令之后创建的composer.json内容：

```
 {
   "name": "yiisoft/yii2-app-basic",
   "description": "Yii 2 Basic Application Template",
   "keywords": ["yii2", "framework", "basic",
   "application template"],
   "homepage": "http://www.yiiframework.com/",
   "type": "project",
   "license": "BSD-3-Clause",
   "support": { 

   "issues": "https://github.com/
           yiisoft/yii2/issues?state=open",
           "forum": "http://www.yiiframework.com/forum/",
           "wiki": "http://www.yiiframework.com/wiki/",
           "irc": "irc://irc.freenode.net/yii",
           "source": "https://github.com/yiisoft/yii2" 

 },
   "minimum-stability": "stable",
   "require": { 
   "php": ">=5.4.0",
           "yiisoft/yii2": "*",
           "yiisoft/yii2-bootstrap": "*",
           "yiisoft/yii2-swiftmailer": "*" 

 },
   "require-dev": { 

   "yiisoft/yii2-codeception": "*",
           "yiisoft/yii2-debug": "*",
           "yiisoft/yii2-gii": "*",
           "yiisoft/yii2-faker": "*" 

 },
   "config": { 
   		"process-timeout": 1800
   }, 

 "scripts": {
           "post-create-project-cmd": [ 

 "yii\\composer\\Installer::postCreateProject"
           ] 

}, "extra": {

 "yii\\composer\\Installer::postCreateProject": {
               "setPermission": [ 

 {
	 "runtime": "0777", 
	 "web/assets": "0777", 
	 "yii": "0755"
 } 

 ],
"generateCookieValidationKey": [ 

 "config/web.php"
               ] 

 },
           "asset-installer-paths": { 

 "npm-asset-library": "vendor/npm", 

 "bower-asset-library": "vendor/bower"
           } 

} }
```
While most of these items (such as the name, description, license, and require blocks) are rather self-explanatory, there are a few Yii2-specic items in here that we should take note of. The rst section we want to look at is the "scripts" section:

大部分内容（例如name,description,license,require blocks)都很容易理解，有一些配置项我们需要关注，首页让我们来看看scripts部分：

```
 "scripts": {
       "post-create-project-cmd": [ 
			 "yii\\composer\\Installer::postCreateProject"
			 ]
}
```
This script tells Composer that when the create-project command is run, it should run the postCreateProject static function. Looking at the the framework source code, we see that this le is referenced in the yii2-composer package (refer to https://github.com/yiisoft/yii2-composer/blob/master/Installer. php#L232). This command then runs several post-project creation actions, namely setting the local disk permissions, generating a unique cookie validation key, and setting some asset installer paths for composer-asset-plugin.

script告诉Composer，在使用create-project命令时，应该执行postCreateProject静态方法。

Next, we have the "extra" block:
```
 "extra": {
       "yii\\composer\\Installer::postCreateProject": { 
			 "setPermission": [
			               { 
			 					"runtime": "0777",
			                   	"web/assets": "0777",
			                   	"yii": "0755" 
			
			} ],

			 "generateCookieValidationKey": [
			 "config/web.php"
			           ] 

 },
       "asset-installer-paths": { 

 "npm-asset-library": "vendor/npm", 

 "bower-asset-library": "vendor/bower"
       } 

}
```
This section tells Composer to use these options when it runs the postCreateProject command. These preconfigured options give us a good starting point to create our applications.

这个部分告诉Composer在执行postCreateProject命令时使用这些参数。这些预定义参加让我们创建应用程序时有一个好的开始。

# 译者说
此部分提前告诉我们Composer这个PHP最新加入的利器，他可以让PHP的开发更具有模块化。让代码利用变得可能，可以说，正是因为Composer的存在，才让PHP语言展现了新的魅力，让PHP开发者在Java等开发者面前扬眉吐气。