# Protect an environment group

You can mark environments as protected in CD4PE, and specify groups of users who are allowed to approve deployments to those environments.  This is similar to how you used to protect branches in your VCS, in order to keep them from being inappropriately deployed.  But with CD4PE, you let **it** do the gating.

First, make a group of approvers, and add yourself to it.

1. On the left-hand, click "Settings"
1. Click "Groups"
1. Click "+ Create Group"
1. Name the group something like "production-approvers"
1. Set the description to something like "People who can approve production promotion"
1. Click "Create group" and then close the dialog
1. Now, click "Puppet Enterprise"
1. In the column for "Protected Environments" click on the number "0"
1. Click "Add"
1. Choose "production"
1. Flip the slider to enable your new group to approve code deployments
1. Click "Add" then "Done"
1. Click "Done" again

Now, we'll kick off the master pipeline and watch it wait for an approval.  There is an important difference between promotion, and environment protection.  Promotion simply tells CD4PE to start evaluating the next *stage*.  Environment protection is enforced as part of the deployment *job*, and is not evaluated when promoting between stages.  This is the long way around to say that it's safe to now set Auto promote between the staging and production jobs, because while the pipeline will go straight from staging to production *stages*, the Production deployment will stop as soon as it sees it needs approval.

1. On the left, click "Control repos" and select your control repository
1. In the "Pipelines" area on the right, use the drop-down to ensure you are looking at the master pipeline
1. Add a checkmark to "Auto promote" between the staging and production stages.

Let's trigger the pipeline with a push to master, and walk through the whole process.  (If you have extra time, make a feature branch, pull request, and merge it.)

1. Switch back to your SSH connection to the CD4PE node
1. Change directories back into your `~/control-repo` directory
1. Make sure you're on the master branch, make a commit, and push it up
1. `git checkout master`
1. `git pull origin master`
1. `git commit -m 'Empty to try protecting environments' --allow-empty`
1. `git push origin master`

This should trigger the pipeline, you can usher it through the whole pipeline now.

1. Switch back to the CD4PE GUI
1. Click "New events"
1. Watch the pipeline run its validation jobs
1. Wait for it to complete its impact analysis
1. Watch it auto promote to Development when those items finish successfully
1. Click "Promote" to move it along to the Staging stage
1. It will report the production branch is "Deployment Running"
1. Click the job number right under the "Deployment Running" text
1. Under "Deployment events" the "Approval task" needs you to click "Approve"
1. Click "Approve" in the ensuing dialog, and then "Done"
1. The pipeline will now continue and deploy the production environment

## Discussion questions

* What sort of conversations will you have with customers who are used to protecting branches, as they switch to protecting environments in CD4PE?
* What if some malicious person just pushes code to the production branch, "bypassing" CD4PE's approval?
