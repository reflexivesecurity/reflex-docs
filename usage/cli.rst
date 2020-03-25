==================================
Using the Cli
==================================

Requirements
----------------------------------
If you haven't yet installed the Reflex CLI, refer to :doc:`/usage/installation`

Usage
----------------------------------
In order to get a list of commands and options type:
::

  reflex

Available Commands
----------------------------------
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


**create**

 ::

  reflex create

- Will walk you through the steps of creating a reflex rule. Creates the directory and all the necessary files to create a rule. Documents which areas need manual intervention in order to make the rule work.

Options
----------------------------------

**--version**

- Show the current version of reflex-cli you have installed.

**--home**

- Allows you to specify a directory to operate on, other then the one you are in currently.

**-v**

- Enable verbose mode.

**--help**

- Show all available commands and options.


