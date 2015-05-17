

ckanapi and ckanext-scheming
----------------------------

CKANCON 2015

Ian Ward

http://datacats.com/

http://open.canada.ca/

http://ckan.org/


ckanapi
-------

https://github.com/ckan/ckanapi

* a python library for calling ckan actions
* a command-line client for calling ckan actions


python library
--------------

* pass strings, lists, dicts, file objects like normal method calls

.. code-block:: python

    import ckanapi

    ckan = ckanapi.LocalCKAN()
    with open('mydata.csv') as csv:
        ckan.action.package_create(name='best-dataset', title='Best evar')
        ckan.action.resource_create(package_id='best-dataset', upload=csv)

safe
----

* raises exceptions on errors, no manual error checking
* clean context and data_dict for every call
* has great test coverage

universal
---------

* python 2.6, 2.7, 3.2, 3.3, 3.4 (source-compatible)
* generic, no per-action custom code
* same interface for use
  * from core or extensions: LocalCKAN
  * for remote API calls: RemoteCKAN
  * in tests: TestAppCKAN

core?
-----

* ckan/lib/cli.py

ckanapi python library
----------------------

.. code-block:: python

    import ckanapi

command-line client
-------------------

* single + bulk actions
* easy to pipeline
* local + remote

single actions
--------------

* pass strings and files as simple parameters

.. code-block:: bash

    ckanapi action package_create name=best-dataset title="Best evar"
    ckanapi action resource_create package_id=best-dataset upload=@mydata.csv

bulk actions
------------

.. code-block:: bash

    ckanapi dump datasets
    ckanapi dump organizations
    ckanapi dump groups

bulk actions
------------

.. code-block:: bash

    ckanapi load datasets
    ckanapi load organizations
    ckanapi load groups

bulk actions
------------

.. code-block:: bash

    ckanapi load datasets -p 6
    ckanapi load organizations -p 6
    ckanapi load groups -p 6

pipelining
----------

.. code-block:: bash

    ckanapi dump datasets | ssh otherbox ckanapi load datasets -p 6

local + remote
--------------

.. code-block:: bash

    ckanapi dump datasets -r http://sourceckan | ckanapi load datasets -p 6
