# Integrate with GitLab

CD4PE should use a service account when integrating with your source control server.  In the interest of time, we've pre-created a service account, "cd4pe" in the GitLab instance, and it owns all participants' control repositories.  We've also created an ssh keypair, supplying it as both the deploy key for Code Manager, and the personal key for the cd4pe user.  (Not safe for work, but fine for a workshop.)  Everyone will use this single cd4pe user in GitLab, to keep things simple.

## Do this

First we'll need to generate a token in the GitLab instance for the cd4pe user.  It doesn't hurt for everyone to try this, the GitLab server will just have a few dozen access tokens issued.

1. Log in to GitLab as "cd4pe" with the password "puppetlabs"
1. Click the icon in the upper-right to expose the drop-down menu, and select "Settings"
1. In the left-hand navigation, choose "Access Tokens"
1. Name it something descriptive, like your name
1. Set the expiration to anything beyond this week
1. Click to checkmark both "api" and "read_user"
1. Click to "Create personal access token"
1. Scroll up to where it says "Your new access token" and copy it

Next we'll use the token to integrate CD4PE with source control.

1. In the CD4PE GUI, click the "Integrate Source Control" button at the top of the window,
    1. (Or if you've dismissed that, click "Settings" then "Source Control")
1. Click "GitLab",
1. Set the "Host" to http://**<gitlab.puppetlabs.vm>** (Note: http not https),
1. Paste the access token that you just generated from GitLab,
1. Click "Add credentials",
1. CD4PE will validate that they work,
1. It will generate an SSH keypair for itself and attach it to the cd4pe user,
1. After validation, you can click "Done" to dismiss the dialog.

## Discussion questions

* Why does the CD4PE user create an SSH key for itself in GitLab, if Code Manager is doing the deploys?
