Customizing Reflex
==================================
While Reflex comes with many features and rules out of the box, there may
be be additional rules and functionality that you desire. Reflex gives
you the ability to customize the functionality of existing rules, as well as
to create your own custom rules.

Adding Custom Functionality
----------------------------------
You are able to customize functionality for all Reflex rules you are using
by customizing the AWSRule class that all Reflex rules inherit.

This allows you to either overwrite or extend the shared methods that Reflex
rules inherit. Additionally, there are multiple hooks you can utilize to 
execute custom code at various points during the execution of a Reflex rule.
This enables you to add additional functionality to Reflex rules without having
to modify the underlying functionality.

Customization Steps
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
1. First, make a copy of the
`aws_rule.py <https://github.com/reflexivesecurity/reflex-core/blob/master/reflex_core/aws_rule.py>`_
module. We recommend storing the copy with your ``reflex.yaml`` configuration.

2. Customize ``aws_rule.py`` by extending and/or overriding its predefined
methods, and/or by using the provided hooks. Hooks are available for before and
after the resource is checked for compliance, and before and after remediation
is performed.

An example is provided below for reference.

.. code-block:: python
    :linenos:

    """ Example customized AWSRule """
    from reflex_core import AWSRuleInterface


    class AWSRule(AWSRuleInterface):
        """This is an example of a customized AWSRule base class"""

        def __init__(self, event):
            super().__init__(event)

            # You can add individual functions
            self.add_pre_compliance_check_functions(self.my_custom_pre_compliance_check_function)
            self.add_post_compliance_check_functions(self.my_custom_post_compliance_check_function)

            # Or a list of one or more functions
            self.add_pre_remediation_functions([self.my_custom_pre_remediation_function])
            self.add_post_remediation_functions([self.my_custom_post_remediation_function])

        def my_custom_pre_compliance_check_function(self):
            # Your custom code here
            return

        def my_custom_post_compliance_check_function(self):
            # Your custom code here
            return

        def my_custom_pre_remediation_function(self):
            # Your custom code here
            return

        def my_custom_post_remediation_function(self):
            # Your custom code here
            return

3. Include your customized ``aws_rule.py`` module in your packaged Reflex rules.
If you're using the ``reflex package`` CLI command to generate your lambda
packages, you can use ``reflex package -m /path/to/custom/aws_rule.py``.

If your customized ``AWSRule`` class requires extra dependencies, you can use
the ``-a`` flag with ``reflex package`` to specify the location of a
``requirements.txt`` file which declares those dependencies and automatically
includes them with your lambda packages.

Creating Custom Rules
----------------------------------
The Reflex CLI provides the ``reflex create`` command for generating the
skeleton of custom Reflex rules. To create custom rules, simply run
``reflex create`` and provide the required information. Once your rule skeleton
has been created, complete the ``TODOs`` in the skeleton code, commit the rule
to GitHub, and add the rule to your ``reflex.yaml`` configuration file. You can
then deploy your rule via the normal deployment process.
::

    cli_version: 1.2.0

    engine_version: v2.1.0

    globals:
        default_email: example@example.com

    backend:
        s3:
        - bucket: my-terraform-state
        - key: reflex-state
        - region: us-east-1

    providers:
    - aws:
        region: us-east-1

    rules:
        aws:
        - custom-reflex-rule-repository-name:
            github_org: github_username
            version: v1.0.0
