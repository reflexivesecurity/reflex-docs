:github_url: https://www.github.com/cloudmitigator/reflex-cli

Installing Reflex
==================================

Dependencies
----------------
To deploy the reflex infrastructure, you will need to use terraform and have an AWS account to deploy to.

Install Python
^^^^^^^^^^^^^^^^^^^^^^^^
If using the CLI, you will need to `install python3. <https://www.python.org/downloads/>`_

Install Terraform
^^^^^^^^^^^^^^^^^^^^^^^^
Reflex uses Terraform under the hood, so you'll need to `install that as well. <https://learn.hashicorp.com/terraform/getting-started/install.html>`_


Set Up AWS Provider
^^^^^^^^^^^^^^^^^^^^^^^^
If you're already launching Terraform with an AWS provider setup, continue using that provider confirguration, otherwise, continue using roles or credentials as:

Reflex currently only supports AWS, so you'll need to setup AWS credentials or a role for Terraform to utilize. For instructions on setting up your credentials see `the AWS documentation. <https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-files.html>`_

CLI Installation
-------------------------
To get started with Reflex, install the Reflex CLI: ``pip install reflex-cli``

Note: when using the system's python3 installation, the above command may be ``pip3 install reflex-cli``. We recommend python environment management via ``pyenv`` or ``pipenv``. 

Terraform Module Integration
----------------------------------
If you'd like to use our reflex terraform modules independently, simply reference them properly as a `git source`__.

.. __: https://www.terraform.io/docs/modules/sources.html#generic-git-repository


As an example of this, the following is the output of a built module using the reflex CLI's ``reflex build`` command:

.. code-block:: terraform

  module "reflex-aws-enforce-s3-encryption" {
    source            = "git::https://github.com/cloudmitigator/reflex-aws-enforce-s3-encryption.git?ref=v0.4.2"
    sns_topic_arn     = module.central-sns-topic.arn
    reflex_kms_key_id = module.reflex-kms-key.key_id
    mode              = ""
  }

For information about the terraform modules, check out the relevant rule or engine repository in our `Github organization`__.

.. __: https://www.github.com/cloudmitigator/
