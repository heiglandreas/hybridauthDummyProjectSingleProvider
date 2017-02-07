# OrgHeiglHybridAuth - DummyImplementation

## Introduction

This is a skeleton application using the Zend Framework MVC layer and module
systems. This application is meant to be used as a starting place for those
looking to get their feet wet with Zend Framework and OrgHeiglHybridAuth.

## Integrating OrgHeiglHybridAuth

The easiest way to integrate OrgHeiglHybridAuth into a Zend Framework project is to use
[Composer](https://getcomposer.org/).  If you don't have it already installed,
then please install as per the [documentation](https://getcomposer.org/doc/00-intro.md).

To integrate OrgHeiglHybridAuth into your existing Zend Framework project:

```bash
$ composer require org_heigl/hybridauth 3.*
```

Then you will need to copy the file ```vendor/org_heigl/hybridauth/config/autoload/module.orgHeiglHybridAuth.test.php```
into your Zend Framework projects ```config/autoload/```-folder with a name that suits your needs.

Edit the newly created configuration-file by adding the informations of at least 
one authentication provider. 

For that you will need to create authentication-tokens at the providers website. 
Usually that involves creating an "app" on the website of your authentication-provider.
For Twitter (as one example) this is https://apps.twitter.com/ - for GitHub (as a second example)
this is https://github.com/settings/applications/new - Those are two examples I will use
to illustrate the usage of the library.

The example config-file contains the following entries: For more possibilities 
have a look at [the HybridAuth documentation]()

```php
'hybrid_auth' => [
    'providers' => [
        'Twitter' => [
            'enabled' => true, 
            'keys' => [
                'key' => '<Consumer Key (API Key)>', 
                'secret' => '<Consumer Secret (API Secret>'
            ]
        ],
        'GitHub' => [
            'enabled' => true,
            'keys' => [
                'key' => '<Client ID>',
                'secret' => '<Client Secret>',
            ]
        ]
    ],
],
'backend' => [
    'twitter',
]
```

Now you can add a menu-item to your layouts menu like this:

```php
<ul class="nav navbar-nav">
    <li class="active"><a href="<?= $this->url('home') ?>">Home</a></li>
    <?= $this->hybridauthinfo('Twitter', $this->serverUrl(true)) ?>
</ul>
```

Note: Only the ```<?= $this->hybridauthinfo('Twitter', $this->serverUrl(true)) ?>``` 
was added. 