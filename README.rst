s2i-thoth-example
-----------------

This is an example S2I application which uses Thoth's recommendations.

Usage
=====

To deploy this application to OpenShift:

.. code-block:: console

  oc process -f openshift.yaml | oc apply -f -

The BuildConfi is using UBI8 Pythpn 3.6 to build the application.

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

  oc delete all --selector 'app=s2i-thoth-example'


Using Thoth in your s2i builds
==============================

To enable Thoth in your s2i builds, copy content of `.s2i` directory present in
this repository into your Git repository which is s2i enabled and remove
`Pipfile.lock` from your repository (locking is left on Thoth based on the
recommendation engine). And thats it!

... optionally you might want to configure thamos client with additional
options by using configuration file template - `see README in thamos repository
<https://github.com/thoth-station/thamos#using-custom-configuration-file-template>`_.

