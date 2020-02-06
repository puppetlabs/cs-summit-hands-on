# Integrate with Puppet Enterprise

CD4PE should use a service account when connecting to Puppet Enterprise.  The account needs to be able to deploy code, make node groups, assign nodes to them, and run Puppet when a direct deployment policy is involved.

In the interest of time, we've pre-created a "cd4pe" user with password "puppetlabs" in your console with the correct permissions.  You can inspect them, if you're curious.  Here's how to integrate CD4PE with Puppet Enterprise.

## Do this

1. In CD4PE, make sure you're logged in as your non-root user,
  1. (The lower left corner says who you're logged in as, and lets you log out.)
1. There's a big set of buttons up top, click "Integrate Puppet Enterprise,"
  1. (If you've dismissed that already, click "Settings" on the left, then "Puppet Enterprise".)
1. Click to "Add Credentials"
1. Supply a name, for instance "main-instance"
1. For the console address, supply the FQDN of your Puppet **Master**
1. Leave the radio box set to "Basic Authorization"
1. Supply the username we already created for you, "cd4pe"
1. Supply the password we already set for the user, "puppetlabs"
1. A token lifetime of 6 months is fine for the workshop, though customers may prefer way longer
1. Click "save changes"
1. CD4PE will now use the credentials.
  1. (And on our short-term support master, it also configures Impact Analysis.)
  1. (On the LTS you would use the cd4pe::impact_analysis class.)

## Discussion questions

* Why bother with a cd4pe service account in the console, instead of just using admin or some user?
* What kind of permissions do you think the service account needs?
