Installation
============

To begin, add the dependent bundles to the ``src/Bundle`` directory. If using
git, you can add them as submodules::

  git submodule add git@github.com:sonata-project/jQueryBundle.git src/Bundle/Sonata/jQueryBundle
  git submodule add git@github.com:sonata-project/BaseApplicationBundle.git src/Bundle/Sonata/BaseApplicationBundle

Next, be sure to enable the bundles in your application kernel:

.. code-block:: php

  // app/AppKernel.php
  public function registerBundles()
  {
      return array(
          // ...
          new Bundle\Sonata\jQueryBundle\SonatajQueryBundle(),
          new Bundle\Sonata\BluePrintBundle\SonataBluePrintBundle(),
          new Bundle\Sonata\BaseApplicationBundle\SonataBaseApplicationBundle(),
          // ...
      );
  }

Configuration
-------------

To use the ``BaseApplicationBundle``, add the following to your application
configuration file.

.. code-block:: yaml

    # app/config/config.yml
    base_application.config: ~

The bundle also contains several routes. Import them by adding the following
code to your application's routing file:

- Add the BaseApplicationBundle's routing definition

.. code-block:: yaml

    # app/config/routing.yml
    base_application:
        resource: BaseApplicationBundle/Resources/config/routing/base_application.xml
        prefix: /admin

    admin:
        resource: base_application
        prefix: /admin

At this point you can access to the dashboard with the url: ``http://yoursite.local/admin/dashboard``.

.. note::

    If you're using XML or PHP to specify your application's configuration,
    the above configuration and routing will actually be placed in those
    files, with the correct format (i.e. XML or PHP).


Declaring new Entity
--------------------

Once you have created an admin class, you must declare the class to use it. Like ::

.. code-block:: yaml

    # app/config/config.yml
    base_application.config:
        entities:
            post:
                label:      Post
                group:      blog
                class:      Bundle\Sonata\NewsBundle\Admin\PostAdmin
                entity:     Application\Sonata\NewsBundle\Entity\Post
                controller: Bundle\Sonata\NewsBundle\Controller\PostAdminController

            tag:
                label:      Tag
                group:      blog
                class:      Bundle\Sonata\NewsBundle\Admin\TagAdmin
                entity:     Application\Sonata\NewsBundle\Entity\Tag
                controller: Bundle\Sonata\NewsBundle\Controller\TagAdminController

            comment:
                label:      Comment
                group:      blog
                class:      Bundle\Sonata\NewsBundle\Admin\CommentAdmin
                entity:     Application\Sonata\NewsBundle\Entity\Comment
                controller: Bundle\Sonata\NewsBundle\Controller\CommentAdminController