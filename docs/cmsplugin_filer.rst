.. _filer:

=======================
filer / cmsplugin-filer
=======================

``djangocms-blog`` uses the ``ThumbnailOption`` model from ``cmsplugin-filer`` / ``django-filer``.

``ThumbnailOption`` model used to be in ``cmsplugin-filer`` up to version 1.0 included.

Since ``cmsplugin-filer`` 1.1 has been moved to ``django-filer`` (since version 1.2).

``djangocms-blog`` introduced compatibility shims to support both combinations.

Since ``djangocms-blog`` 1.0 the compatibility has been dropped and ``django-filer`` 1.3 is required
for ``djangocms-blog`` to work.

See below the migration path if you still use older versions of ``cmsplugin-filer`` / ``django-filer``.

*****************************************
Upgrading cmsplugin-filer from 1.0 to 1.1
*****************************************

Due to changes in ``cmsplugin-filer`` / ``django-filer`` which moved
``ThumbnailOption`` model from the former to the latter, ``djangocms-blog``
must be migrated as well.

Migrating cmsplugin-filer to 1.1 and djangocms-blog up to 0.8.4
===============================================================

If you have djangocms-blog up to 0.8.4 (included) installed or you are upgrading from a previous
djangocms-blog version together with cmsplugin-filer upgrade, you can just apply the migrations::

    pip install cmsplugin-filer==1.1.3 django-filer==1.2.7 djangocms-blog==0.8.4
    python manage.py migrate

Migrating cmsplugin-filer to 1.1 and djangocms-blog 0.8.5+
==========================================================

If you already a djangocms-blog 0.8.5+ up to 0.8.11, upgrade to 0.8.11, then
you have to de-apply some blog migrations when doing the upgrade::

    pip install djangocms-blog==0.8.11
    python manage.py migrate djangocms_blog 0017 ## reverse for these migration is a noop
    pip install cmsplugin-filer==1.1.3 django-filer==1.2.7
    python manage.py migrate

After this step you can upgrade to 0.8.12::

    pip install djangocms-blog==0.8.12

.. note:: de-apply migration **before** upgrading cmsplugin-filer. If running before upgrade, the
          backward migration won't alter anything on the database, and it will just allow the code
          to migrate ``ThumbnailOption`` from cmsplugin-filer to filer

.. note:: If you upgrade in a Django 1.10 environment, be sure to upgrade both packages
          at the same time to allow correct migration dependencies to be evaluated.

Installing djangocms-blog in an existing project with Django 1.10
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

If your project has cmsplugin-filer 1.1+ already installed and it uses Django 1.10,
install djangocms-blog 0.8.12 (and above)::

    pip install djangocms-blog==0.8.12
