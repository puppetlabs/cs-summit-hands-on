# Create accounts and a workspace

Once the docker container is running, it's time to set-up your CD4PE instance.  Most of the configuration is done in CD4PE's graphical interface.  The `puppetlabs-cd4pe` module sets up the software components and their connections, but the rest of it is up to you in the GUI.

We're going to do two things here.  First you're going to configure the "root" account, which is responsible for overall management of the CD4PE instance.  Then you're going to create a user account, and a corresponding workspace.  A workspace is the area where a team integrates its own VCS, PE, control repository, and modules.  This way several teams can share a CD4PE infrastructure, but only interact with their own resources.

## Do this

1. Browse to http://**<cd4peX.puppetlabs.vm>**:8080/
1. Click the friendly button to "Get Started"
1. You'll be asked to supply an email address and password for the root account
  1. There is no email validation, so it's safe to set something like `root@puppetlabs.vm`
1. Now you'll be asked to configure endpoints, which are all on your CD host with the default ports.  Fill these in and save the settings.
  1. WebUI: http://**<cd4peX.puppetlabs.vm>**:8080/
  1. Backend Service: http://**<cd4peX.puppetlabs.vm>**:8000/
  1. Agent Service: dump://**<cd4peX.puppetlabs.vm>**:7000/ (Note: dump protocol)
1. Next you'll specify an object store, we'll just use the CD4PE host's local Disk (the default and recommended for Jumpstarts) and we'll leave the name set to "cd4pe".  Click to save those default settings.
1. You'll be asked for a license.  Tell it to run in Trial Mode.
1. Accept the license agreement without reading it or consulting an attorney

Okay, we're halfway there.  When you're ready, proceed to create a normal user account, which you'll use for most of the rest of the configuration.

1. Click to "Create your user account,"
  1. Fill in name, email, username, and password.  As before, there is no email validation so it's safe to set it to something fun like `kermit@puppetlabs.vm`,
1. Since this is a new install, you'll need to click to "Add New Workspace,"
1. Give it any name you like, for instance `muppet-show`,
1. **Stop here** -- we'll integrate all the components next.

## Discussion questions

* Why is there a separate root user and individual users?
* Why might I want to use multiple workspaces?
