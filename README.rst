s2i-thoth-example
-----------------

This is an example s2i application which uses Thoth's recommendations in OpenShift.

Usage
=====

To deploy this application to OpenShift:

.. code-block:: console

  oc process -f openshift.yaml | oc apply -f -

A pre-requirement for this application is a centos:7 python image (Python3.6 s2i).

Once the templates get applied, a build is started. As there is no
``Pipfile.lock`` present (no locked dependencies), Thoth is contacted (see
``.thoth.yaml`` configuration file for info on configuration options).

Thoth computes recommendations and gives back a ``Pipfile.lock`` with
additional guidance on software stack (see build logs). Note that computing
recommendations takes some time, there is assigned certain amount of CPU based
on Thoth's backend configuration. Results are cached (3 hours by default) so
next builds are faster (unless forced or any configuration change on client
side).

To remove this application from OpenShift:

.. code-block:: console

  oc delete all --selector 'app=downshift'
