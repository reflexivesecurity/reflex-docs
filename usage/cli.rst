:github_url: https://www.github.com/cloudmitigator/reflex-cli

==================================
Reflex CLI
==================================

Usage
----------------------------------
In order to get a list of commands and options type:
::

  reflex

Available Commands
^^^^^^^^^^^^^^^^^^^
**init:**

 ::

  reflex init

- Initialize the current directory with a configuration file. This will prompt you to give an email, aws region, backend and then prompt you for the different rules you might want. After this completes you will have a reflex.yaml containing the information given from earlier.

**build**

 ::

  reflex build

- Utilize the reflex.yaml to grab all the rules specified as well as the necessary Terraform scaffolding to setup the rules. Creates a reflex_out directory with the necessary terraform files.

**show**

 ::

  reflex show

- Will show all possible reflex rules, and the latest version of the rules.

**region**

 ::

  reflex region

- Will provision region infrastructure build directory when passed a valid region with `--region`. 


**create**

 ::

  reflex create

- Will walk you through the steps of creating a reflex rule. Creates the directory and all the necessary files to create a rule. Documents which areas need manual intervention in order to make the rule work.

Options
^^^^^^^^^^^

**--version**

- Show the current version of reflex-cli you have installed.

**--home**

- Allows you to specify a directory to operate on, other then the one you are in currently.

**-v**

- Enable verbose mode.

**--help**

- Show all available commands and options.

Reflex Config File: reflex.yaml
----------------------------------
The generated asset of ``reflex init`` is a config file which is by default named ``reflex.yaml``. Below is a reference for the format of that file:

.. code-block:: yaml

  ---
  cli_version: '1.0'


  engine_version: v1.0.0


  globals:
    default_email: administrator@example.com


  backend:
    s3:
    - bucket: example-backend-bucket
    - key: reflex-state


  providers:
  - aws:
      region: us-east-1


  rules:
    aws:
    - enforce-s3-encryption:
        configuration:
        - mode: detect
        version: v0.4.2
    - detect-deactivate-mfa:
        version: v0.3.3
    - detect-root-user-activity:
        version: v0.2.4
    - enforce-no-public-ami:
        configuration:
        - mode: detect
        version: v0.3.2
    - custom-reflex-rule-repository-name:
        configuration:
        - github_org: github_username
        version: v0.0.2
