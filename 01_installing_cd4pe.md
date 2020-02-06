# Installing CD4PE with the `puppetlabs-cd4pe` module

Installing CD4PE is best done using the `puppetlabs-cd4pe` module.  Since the module allows you to mess with parameters and re-run the Puppet agent, it's a way better option than trying to get the task-based parameters right on the first shot and then hand-edit things to get it working.  We work at Puppet, after all; scripts do not become us.

The module does a few things for you, to get CD4PE up and running with its necessary additional components.

* Installs Docker, using the puppet-docker module,
* Installs pe-postgresql, using the puppet_enterprise modules, and
* Pulls down the CD4PE docker container and starts it.

Your control repository already has this module and its dependencies in its Puppetfile, so installing CD4PE on a node is simply a matter of classifying the node.  The documentation has us do this in the console, and that seems a reasonable approach for most new customers.

## Do this

1. Log in to your Enterprise Console as "admin" with password "puppetlabs",
1. Pop into "Classification" and create a "PE Continuous Delivery" node group with a parent of "PE Infrastructure" and the rest defaults,
1. Click to add membership rules, and pin your CD4PE host to the group,
1. Switch to the "Configuration" tab and add the `cd4pe` class to your node.
  1. Set the `cd4pe_version` parameter to `"3.x"` so that you get the newest version.  (Setting `latest` actually gets you the latest in the 2.x series.)
  1. Leave the rest of the parameters as they are.
1. Commit your changes and run Puppet on the CD4PE host
  1. Watch it install docker and pe-postgresql.
  1. Tail `/var/log/messages` after the run to see docker pull down the CD4PE docker image and start it up, and
1. After a minute or two, browse to http://**<cd4peX.puppetlabs.vm>**:8080/ once the docker container is finally up.  (Note: http and port 8080)
1. **Stop here** -- we'll do the initial setup next.

## Discussion questions

* Why use a module instead of the simple Bolt task?
* How can I get a newer minor version of CD4PE when they release it?
