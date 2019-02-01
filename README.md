# Ansible infrastructure
Ansible infrastructure

Thoughts about infrastucture:

* Ansible is fine for setting up infrastcutre that is not in a part of an ongoing development - e.g netbox or consul
* Coreos ignition templates for immutable infrastructure services like bitcoin, ipam provisioners etc. that are part of ongoing development
* When coreos ignition files are used, than ansible is used for test only with --check --diff to see everything is as espected. This also sets an test driven development

##  Service discovery:

* Use consul as service discovery for dynamic inventory. TTL will also remove stale infrastructure

##Do we really need provisioning in the cloud?
Instead of using the empty AMIs you could bake your own AMI and skip the whole provisioning part completely but I see a giant flaw in this setup. Every change, even a small one, requires recreation of the whole instance. If it’s a change somewhere on the base level then you’ll need to recreate your whole fleet. It quickly becomes unusable in case of deployment, security patching, adding/removing a user, changing config and other simple things.

Even more so if you bake your own AMIs then you should again provision it somehow and that’s where things like Ansible appears again. My recommendation here is again to use Packer with Ansible.

So in the most cases, I’m strongly for the provisioning because it’s unavoidable anyway.

# How to use Ansible with Terraform
Now, returning to the actual provisioning I found 3 ways to use Ansible with Terraform after reading the heated discussion at this GitHub issue. Read on to find the one that’s most suitable for you.




