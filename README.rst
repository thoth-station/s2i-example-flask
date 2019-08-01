Thoth's Flask stack guidance example
------------------------------------

.. note::

   For a deeper look into details, please use `s2i-example-tensorflow
   <https://github.com/thoth-station/s2i-example-tensorflow>`_  which is a
   maintained reference of Thoth's s2i example.

This is an example of OpenShift's s2i (source-to-image) application which uses
Thoth's recommendations to recommend a Flask stack for a specific hardware
where Flask application is supposed to be run together with software
environment (base image).

The application is showing a generic approach and how to integrate inside
OpenShift's s2i build process. To have recommendations suited for your specific
hardware, you need to configure the build to be done on specific hardware where
the application is supposed to be run (specific node placement for build and
application run which should match).

Usage
=====

To deploy this application to OpenShift:

.. code-block:: console

  oc project <YOUR-PROJECT-NAME>
  oc process -f openshift.yaml | oc apply -f -

After applying the templates, the build should be started. As there is no
``Pipfile.lock`` provided, Thoth is contacted to give guidance for the deployed
application. Computing recommendations for the application stack used in this
application takes approximately 10 seconds - the time after which you get back
recommendations varies based on the load and deployment you are contacting.

To remove this application from OpenShift:

.. code-block:: console

  oc delete all --selector 'app=s2i-example-flask'

Additional information
======================

Please take a look at `s2i-example-tensorflow
<https://github.com/thoth-station/s2i-example-tensorflow>`_ which has
additional info and documented configuration options. The
s2i-example-tensorflow repo is also better maintained and kept up-to-date.

