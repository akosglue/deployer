<!-- DO NOT EDIT THIS FILE! -->
<!-- Instead edit recipe/contao.php -->
<!-- Then run bin/docgen -->

# How to Deploy Contao

[Source](/recipe/contao.php)

## How to deploy a Contao project with zero downtime?

- First, [install](/docs/installation.md) the Deployer. 
- Second, require `recipe/contao.php` recipe into your _deploy.php_ or _deploy.yaml_ file.
- Third, now you can have a zero downtime deployment!

Did you know that you can deploy **Contao** project with a single command? Just execute `dep deploy`.
Something went wrong? Just run `dep rollback` to rollback your changes.
Also, you can take an advantages of the [Deployer's CLI](/docs/cli.md) to deploy your project.

Another feature of the Deployer is [provisioning](/docs/recipe/provision.md). Take any server, and run `dep provision` command.
This command will configure webserver, databases, php, ssl certificates, and more. 
You will get everything you need to run your **Contao** application.

Deployer does next steps to [deploy](#deploy) **Contao**:
* Displays info about deployment
* Prepares host for deploy
* Locks deploy
* Prepares release
* Updates code
* Creates symlinks for shared files and dirs
* Makes writable dirs
* Installs vendors
* Enable maintenance mode
* Run Contao migrations
* Disable maintenance mode
* Creates symlink to release
* Unlocks deploy
* Cleanup old releases


The contao recipe is based on the [symfony](/docs/recipe/symfony.md) recipe.

## Configuration
### public_path
[Source](https://github.com/deployphp/deployer/blob/master/recipe/contao.php#L11)

Overrides [public_path](/docs/recipe/provision/website.md#public_path) from `recipe/provision/website.php`.

The public path is the path to be set as DocumentRoot and is defined in the `composer.json` of the project
but defaults to `public` from Contao 5.0 on.
This path is relative from the [current_path](/docs/recipe/common.md#current_path), see [`recipe/provision/website.php`](/docs/recipe/provision/website.php#public_path).



### bin/console
[Source](https://github.com/deployphp/deployer/blob/master/recipe/contao.php#L29)

Overrides [bin/console](/docs/recipe/symfony.md#bin/console) from `recipe/symfony.php`.





### contao_version
[Source](https://github.com/deployphp/deployer/blob/master/recipe/contao.php#L33)






## Tasks

### contao:migrate
[Source](https://github.com/deployphp/deployer/blob/master/recipe/contao.php#L47)

Run Contao migrations.

This task updates the database. A database backup is saved automatically as a default.

To automatically drop the obsolete database structures, you can override the task as follows:

```php
task('contao:migrate', function () {
    run('{{bin/php}} {{bin/console}} contao:migrate --with-deletes {{console_options}}');
});
```


### contao:manager:download
[Source](https://github.com/deployphp/deployer/blob/master/recipe/contao.php#L53)

Download the Contao Manager.

Downloads the `contao-manager.phar.php` into the public path.


### contao:install:lock
[Source](https://github.com/deployphp/deployer/blob/master/recipe/contao.php#L59)

Lock the Contao Install Tool.

Locks the Contao install tool which is useful if you don't use it.


### contao:manager:lock
[Source](https://github.com/deployphp/deployer/blob/master/recipe/contao.php#L65)

Lock the Contao Manager.

Locks the Contao Manager which is useful if you only need the API of the Manager rather than the UI.


### contao:maintenance:enable
[Source](https://github.com/deployphp/deployer/blob/master/recipe/contao.php#L71)

Enable maintenance mode.




### contao:maintenance:disable
[Source](https://github.com/deployphp/deployer/blob/master/recipe/contao.php#L86)

Disable maintenance mode.




### deploy
[Source](https://github.com/deployphp/deployer/blob/master/recipe/contao.php#L98)

Deploy the project.




This task is group task which contains next tasks:
* [deploy:prepare](/docs/recipe/common.md#deployprepare)
* [deploy:vendors](/docs/recipe/deploy/vendors.md#deployvendors)
* [contao:maintenance:enable](/docs/recipe/contao.md#contaomaintenanceenable)
* [contao:migrate](/docs/recipe/contao.md#contaomigrate)
* [contao:maintenance:disable](/docs/recipe/contao.md#contaomaintenancedisable)
* [deploy:publish](/docs/recipe/common.md#deploypublish)

