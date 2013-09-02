# Twitter Bootstrap 3 Bundle for Symfony2

## Current Version

Bootstrap 3.0.0

## Installation

### Add bundle to your composer.json file

``` js
// composer.json

{
    "require": {
        // ...
        "pinano/bootstrap3-bundle": "dev-master"
    }
}
```

### Or, if you prefer, choose a specific version

``` js
// composer.json

{
    "require": {
        // ...
        "pinano/bootstrap3-bundle": "3.0.0"
    }
}
```

### Add bundle to your application kernel

``` php
// app/AppKernel.php

public function registerBundles()
{
    $bundles = array(
        // ...
        new Pinano\Bootstrap3Bundle\PinanoBootstrap3Bundle(),
        // ...
    );
}
```

### Download the bundle using Composer

``` bash
$ php composer.phar update pinano/bootstrap3-bundle
```

### Install assets

Given your server's public directory is named "web", install the public vendor resources

``` bash
$ php app/console assets:install web
```

Optionally, use the --symlink attribute to create links rather than copies of the resources

``` bash
$ php app/console assets:install --symlink web
```

Notes: All the urls of the original routes have been changed to '../images/*' due to Bundle package requirements.

## Usage

Once you have imported all the resources to the vendor folder, you can self-import the JS into your Symfony project as usual with:


``` twig
{% block javascripts %}
    {% javascripts
        ...
        '@PinanoBootstrap3Bundle/Resources/public/js/bootstrap.js'
        ...
        %}
        <script src="{{ asset_url }}"></script>
    {% endjavascripts %}
{% endblock %}
```

And with the CSS as well using with:
``` twig
{% block stylesheets %}
    {% stylesheets filter='cssrewrite'
      'bundles/pinanobootstrap3/css/bootstrap.css'
      'bundles/pinanobootstrap3/css/bootstrap-theme.css'
    %}
        <link rel="stylesheet" href="{{ asset_url }}" />
    {% endstylesheets %}
{% endblock %}
```
Note: See https://github.com/kriswallsmith/assetic/issues/53 for known limitations of assetic with CSS referencing.

## Licenses

I do not own Bootstrap 3 files at all, I'm just providing a Bundle package to easy-install them all. Refer to the source code of the included files from Bootstrap 3 for license information.

## References

1. http://getbootstrap.com/
2. http://symfony.com
