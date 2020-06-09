:github_url: https://www.github.com/cloudmitigator/reflex-cli

Managing Reflex Infrastructure
===========================================

Deploying Reflex Infrastructure
---------------------------------
Refer to our generating and deployment documentation in the :doc:`/usage/quickstart` for how to work with our terraform output.

Applying Updates
--------------------------------
As our cloud environments change, there will inevitably be updates to our Reflex infrastructure and the addition of new security rules. By leveraging terraform, we can update our built terraform modules with a simple call to ``terraform apply``. 

Removing Reflex Infrastructure
--------------------------------
Similarly, to remove reflex infrastructure, simply run ``terraform destroy``. 
