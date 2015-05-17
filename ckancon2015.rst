

ckanapi and ckanext-scheming
----------------------------


ckanapi
-------


* a python library for calling ckan actions
* a command-line client for calling ckan actions


python library
--------------

* pass strings, lists, dicts, file objects like normal method calls

... code-block:: python

    ckan = ckanapi.LocalCKAN()
    with open('mydata.csv') as csv:
        ckan.action.package_create(name='best-dataset', title='Best evar')
        ckan.action.resource_create(package_id='best-dataset', upload=csv)

safe
----

* raises exceptions on errors, no manual error checking
* great test coverage

universal
---------

* python2 + python3 (source-compatible)
* generic, no per-action custom code
* same interface for use
  * from core or extensions: LocalCKAN
  * for remote API calls: RemoteCKAN
  * in tests: TestAppCKAN


