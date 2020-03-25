Installing Reflex
==================================

CLI Installation
-------------------------
To get started with Reflex, install the Reflex CLI: ``pip install reflex-cli``

Terraform Module Integration
----------------------------------
If you'd like to use our reflex terraform modules independently, simply reference them properly as a `git source`__.

.. __: https://www.terraform.io/docs/modules/sources.html#generic-git-repository


As an example of this, the following is the output of a built module using the reflex CLI's ``reflex build`` command:

.. code-block:: hcl

  module "reflex-aws-enforce-s3-encryption" {
    source            = "git::https://github.com/cloudmitigator/reflex-aws-enforce-s3-encryption.git?ref=v0.4.2"
    sns_topic_arn     = module.central-sns-topic.arn
    reflex_kms_key_id = module.reflex-kms-key.key_id
    mode              = ""
  }

For information about the terraform modules, check out the relevant rule or engine repository in our `Github organization`__.

.. __: https://www.github.com/cloudmitigator/
