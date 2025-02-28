ABANDONED
=========

Check this PR to get more info: https://github.com/tzulberti/django-datefilterspec/pull/17



.. image:: https://travis-ci.org/tzulberti/django-datefilterspec.svg?branch=master
    :alt: Build status
    :target: https://travis-ci.org/tzulberti/django-datefilterspec

django-daterange-filter
=======================

Add the option to filter by a custom date range on the admin. This allows
to inputs to be used to get the custom date range filters.

See datefilter.png of a screenshot of how this is seen on the admin.

**IMPORTANT:** this will work with Django 1.4. I won't work with previous Django
versions.

Installation
------------

Use pip/easy_install

.. code-block:: bash

    pip install django-daterange-filter


Add daterange_filter to settings.INSTALLED_APP. For this, edit the setup.py
file:

.. code-block:: python

    INSTALLED_APPS = (
        ...
        'daterange_filter'
    )

For the transitions you need to add JavaScriptCatalog to your urls.py in your project:
file:

.. code-block:: python

    urlpatterns = i18n_patterns(
        ...
        path('jsi18n/', JavaScriptCatalog.as_view(), name='javascript-catalog'),
    )

After this, if you have a model like this one:

.. code-block:: python

    class MyModel(models.Model):
        ...
        foo = models.CharField(max_length=1, choices=BAR_CHOICES)
        created_at = models.DateField()
        

To allow to filter the **created_at** field using the date ranges, you must
edit the admin.ModelAdmin referenced to that class:

.. code-block:: python

    from daterange_filter.filter import DateRangeFilter
    from django.contrib import admin
    from models import MyModel

    class MyModelAdmin(admin.ModelAdmin):
        list_filter = (
            'foo',
            ('created', DateRangeFilter), # this is a tuple
            ...
        )


DateRangeFilter honours localization and supports local date 
formats for filtering.

Running tests
-------
First :code:`pip install -r requirements.txt`, then :code:`python ./runtests.py`

If you wanna run tests on all supported Python/Django versions, execute :code:`tox`.

Changes 
-------

1.3.0:

* Fixed calendar icon moving to a new line in Django 1.9 (Special thanks to https://github.com/farooqaaa)
* fix daterange_filter function (Special thanks to https://github.com/ZamorakLin)

1.1.1:

* Special thanks to: https://github.com/mightygraf

0.2.0:

* Updated README
* Works with DateTime (special thanks to Andrea Rabbaglietti)

0.1.1:

* Removed the custom DateRangeField
* Improved i18n
* Special thanks to: https://github.com/DXist
