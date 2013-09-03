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

## Usage

Once all the resources are in place, if you want to use the Bootstrap 3 javascript features (modals, dropdowns, etc.) you can edit any of your twig views or layouts to include the Bootstrap3 javascript files. If you don't want to use any of these features you can skip this step. Please refer to the [Bootstrap 3 documentation](http://getbootstrap.com/javascript/) to see what features are available.

Note: Bootstrap 3 javascript resources require that you have previously loaded jQuery library.

``` twig
{% block javascripts %}
    <script src="//ajax.googleapis.com/ajax/libs/jquery/2.0.3/jquery.min.js"></script>
    {% javascripts
        ...
        '@PinanoBootstrap3Bundle/Resources/public/js/bootstrap.js'
        ...
        %}
        <script src="{{ asset_url }}"></script>
    {% endjavascripts %}
{% endblock %}
```

Then you will want to load the css resources to take advantage of the grid and all the responsive utilities.

Note: The bootstrap-theme.css file is optional and is only intended to make Bootstrap 3 look nice out-of-the-box..

``` twig
{% block stylesheets %}
    {% stylesheets filter='cssrewrite'
      ...
      'bundles/pinanobootstrap3/css/bootstrap.css'
      'bundles/pinanobootstrap3/css/bootstrap-theme.css'
      ...
      'bundles/yourawesomebundle/css/awesomestylesheet.css'
      ...
    %}
        <link rel="stylesheet" href="{{ asset_url }}" />
    {% endstylesheets %}
{% endblock %}
```

If you want to create your own LESS mix-ins or variables, you should import Bootstrap 3 LESS files instead of the CSSs and create a css output using any of the LESS filters available ([lessphp](https://github.com/leafo/lessphp) or [nodejs](http://www.kiwwito.com/article/less-css-with-assetic-and-symfony-2) are the ones I know of):
``` twig
{% block stylesheets %}
    {% stylesheets filter='cssrewrite,less'
      ...
      'bundles/pinanobootstrap3/less/bootstrap.less'
      'bundles/pinanobootstrap3/less/theme.less'
      ...
      'bundles/yourawesomebundle/less/awesomestylesheet.less
      ...
    %}
        <link rel="stylesheet" href="{{ asset_url }}" />
    {% endstylesheets %}
{% endblock %}
```

Note: See https://github.com/kriswallsmith/assetic/issues/53 for known limitations of assetic with CSS referencing.

I usually follow a simple inheritance schema when it comes to designing twig templates. That is, I have an app/views/base.html.twig file that I use as a site-wide template. Then, inside every bundle I have my own Resources/views/layout.html.twig file that extends the base template. Depending on the kind of application I'm designing I can place the Bootstrap stuff in the site-wide or the bundle-wide template. Then every view of a given bundle will extend the corresponding bundle layout.html.twig file, which in turn extends the site-wide template.

The folks at Sensio Labs have already covered this approach and you can check it in their [documentation](http://twig.sensiolabs.org/doc/templates.html#template-inheritance).

## Licenses

I do not own Bootstrap 3 files at all, I'm just providing a Bundle package to easy-install them all. Refer to the source code of the included files from Bootstrap 3 for license information.

## References

1. http://getbootstrap.com/
2. http://symfony.com
