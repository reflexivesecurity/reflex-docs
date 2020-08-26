Reflex Quickstart
==================================

Getting started with Reflex is easy, and can be done in as little as 10 minutes.


Install the Reflex CLI
----------------------------------
Installing reflex is generally as simple as running ``pip install reflex-cli``
with a python3 pip.

For further information on installation, refer to :doc:`/installation`


Generating a Reflex Configuration
----------------------------------
Now that everything is installed and configured we can get started using Reflex.
The first step is to create a Reflex configuration file, which tells Reflex
which measures you want to enforce in your environment. The Reflex CLI makes
this easy with the ``init`` command.

Before doing this we recommend you create a new directory to store your Reflex
files. ``mkdir my_reflex_measures`` to create a directory and ``cd
my_reflex_measures`` to switch into it.

Run ``reflex init`` from the command line and you'll be prompted to select which
measures you'd like to enforce in your environment. Proceed through the prompts,
and once you're done the CLI will output a ``reflex.yaml`` configuration file in
the current working directory.


Generating Lambda Deployment Packages
-------------------------------------
Once you've created a ``reflex.yaml`` configuration file, you need to generate
`AWS Lambda Deployment Packages
<https://docs.aws.amazon.com/lambda/latest/dg/python-package.html>`_. Run
``reflex package`` to generate a deployment package for each Rule in your
configuration file. These files will be created in a new ``package_build``
directory by default. (Note: it is possible to generate the deployment packages
yourself, but this is not recommended.)


Generating Terraform Modules
----------------------------------
Once you've created a ``reflex.yaml`` configuration file, you're ready to
generate Terraform modules. Run ``reflex build`` to generate your Terraform
modules. This will output a Terraform file for each measure you have specified
in your configuration. These files will be created in a new ``reflex_out``
directory by default, but this is configurable with the ``-o`` option.

Deploy With Terraform
------------------------

Run Terraform Init
^^^^^^^^^^^^^^^^^^^^^
Once you've generated your Terraform files, you're ready to start deploying your
resources. First run ``terraform init`` from your ``reflex_out`` directory (or
whatever you decided to name it). This will download all the required modules
and perform all steps necessary to deploy your resources.

Run Terraform Plan (Optional)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Once you've generated your Terraform files and run ``terraform init`` you're
ready to deploy your resources. If you want to see what resources will be
deployed before you go ahead, you can run ``terraform plan`` to get a list of
what resources will be added to your environment. Each measure will create
multiple resources, so don't be alarmed that the number of resources being
created is much larger than the number of measures you selected.

Run Terraform Apply
^^^^^^^^^^^^^^^^^^^^^^^^
If you are ready to move forward and actually deploy your resources, go ahead
and run ``terraform apply``, and Terraform will start deploying resources to
your environment. As soon as it finishes running, your resources a deployed and
you're done!
