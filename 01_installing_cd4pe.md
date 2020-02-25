# Installing CD4PE with the `puppetlabs-cd4pe` module

Installing CD4PE is best done using the `puppetlabs-cd4pe` module.  Since the module allows you to mess with parameters and re-run the Puppet agent, it's a way better option than trying to get the task-based parameters right on the first shot and then hand-edit things to get it working.  We work at Puppet, after all; scripts do not become us.

The module does a few things for you, to get CD4PE up and running with its necessary additional components.

* Installs Docker, using the puppet-docker module,
* Installs pe-postgresql, using the puppet_enterprise modules, and
* Pulls down the CD4PE docker container and starts it.

Your control repository already has this module and its dependencies in its Puppetfile, so installing CD4PE on a node is simply a matter of classifying the node.  The documentation has us do this in the console, and that seems a reasonable approach for most new customers.

## Do this

1. Log in to your Enterprise Console (https://summitX-masterY.classroom.puppet.com) as "admin" with password "puppetlabs",
1. Pop into "Classification" and create a "PE Continuous Delivery" node group with a parent of "PE Infrastructure" and the rest defaults,
1. Click to add membership rules, and pin your CD4PE host (cd4peY.classroom.puppet.com) to the group (Note, it lacks the "summitX" part)
1. Switch to the "Configuration" tab and add the `cd4pe` class to your node.
    1. Set the `cd4pe_version` parameter to `"3.x"` -- making sure to use double quotes -- so that you get the newest version.  (Setting `latest` actually gets you the latest in the 2.x series.)
1. Commit your changes and run Puppet on the CD4PE host
    1. Use the console to do the run, or ssh in an run from the command line.
        1. (ssh -i training.pem -l centos summitXcd4peY.classroom.puppet.com)
        1. (sudo /opt/puppetlabs/bin/puppet agent --test)
    1. Watch it install docker and pe-postgresql.
    1. Tail `/var/log/messages` after the run to see docker pull down the CD4PE docker image and start it up, and
1. After a minute or two, browse to http://**summitX-cd4peY.classroom.puppet.com**:8080/ once the docker container is finally up.  (Note: http and port 8080)
1. **Stop here** -- we'll do the initial setup next.

## Discussion questions

* Why use a module instead of the simple Bolt task?
* How can I get a newer minor version of CD4PE when they release it?

---

[Previous - 00 Workshop Environment](00_workshop_environment.md) |  [Next - 02 Create Accounts](02_create_accounts.md)
