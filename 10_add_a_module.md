# Add a module

If you keep your modules in their own individual repositories, you can have CD4PE manage their deployment.  Just like the control repository, they will have pipelines to validate code, run Impact Analysis, and deploy to environments.  Pushing a feature branch even causes CD4PE to make a corresponding branch in the control repository and deploy it, saving you a few manual steps.

## Do this

1. Switch over to the CD4PE GUI
1. In the left-hand navigation, select "Modules"
1. Over on the right, click "Add Module"
1. Choose GitLab as he source
1. Choose the CD4PE organization
1. Select your numbered "puppet-mymodule-**NN**" repository
1. Click "Add"
1. It should detect the .cd4pe.yaml file, click "Yes, manage as code"

Now let's make sure the Pipelines are working as advertised.  In the interest of time, we'll just push a commit to the master branch.  (If you have extra time, try the full workflow of creating a feature branch, pushing it, running an agent against it, creating a pull request, and then merging it.)

1. Switch to your SSH connection on the CD4PE node
1. Change directories into your `~/puppet-mymodule` directory
1. Make an empty commit to master and push it
1. `git commit -m 'Empty for direct push to master' --allow-empty`
1. `git push origin master`
1. Switch back to the CD4PE GUI
1. Click "New events" and watch the pipeline run through the Development deployment
1. Click the "Promote" button, to deploy to Staging and watch it go
1. Click the "Promote" button, to deploy to Production

## Discussion questions

* Suppose several teams have to cooperate on a single "profile" module, but they have to promote their changes at different velocities.  How might breaking out profiles into team-specific modules make this manageable?
