# The workshop environment

Every participant has a sandbox that's been set up to look like the goal of our non-CD4PE-jumpstarts.  Each person has a monolithic master running, and Code Manager configured to pull code from a version control system.  Everyone has their own control repository.  All we have to do from here is install and configure CD4PE.

Your two servers and two repositories are named with your participant number tacked on the end.  You are in either summit group 1 or 2.  In the examples below, X represents your summit number, and Y represents your student number.

* **summitXmasterY**: Your own EL 7 server with a monolithic Puppet Enterprise 2019.2 master already installed on it, and code manager configured.  (But no webhook to trigger it.  We'll let CD4PE trigger it.)

* **summitXcd4peY**: Your own EL 7 server with the Puppet agent installed and checking in to the master.  This is where we'll install CD4PE and it will also double as job hardware.

* **control-repo-X**: Your own control repository in a shared GitLab server.
  * (Originally cloned from https://github.com/puppetlabs/cs-summit-cd-control-repo)

* **puppet-mymodule-X**: Your own module repository in a shared GitLab instance.
  * (Originally cloned from https://github.com/puppetlabs/cs-summit-cd-mymodule)

---

[Next - 01 Installing CD4PE](01_installing_cd4pe.md)
