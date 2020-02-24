# Create and merge a pull request

Finally, we're ready to complete the development cycle by creating a pull request, and then merging it.  First, create the pull request.

1. Log in to the GitLab server as "cd4pe" with the password "puppetlabs"
1. Select your control repository's project
1. Most likely near the top of the project's main page shows your feature branch with a convenient "Create merge request" button.
    1. (If not, in the left-hand pane click "Merge Requests" then "New merge request")
        1. Set the source branch to your feature branch
        1. Confirm the target is "master" (Don't follow your reflex and choose "production")
        1. Select "compare branches and continue"
1. On the ensuing page, click to "Submit merge request"
1. **Don't merge yet.**

As you created the merge request, the webhook notified CD4PE of it.  Watch as the pipeline goes.

1. Switch to the CD4PE GUI
1. In the control repo page, click to see "New events"
1. Note that there are only four validation jobs, and a queued Impact Analysis, but no deployments, because this is just a Pull Request
1. Let the pipeline continue, and watch it stop right when it hits the pull request gate.

Now we're ready to merge.  Since a merge is just a commit the Pull Request Gate will *not* stop the pipeline from continuing past it.

1. Switch back to the GitLab interface
1. Verify that GitLab reflects success of the validation stage right in the merge request
1. Click to Merge your request
1. Switch back to the CD4PE GUI
1. Select "New events"
1. Watch your pipeline run up until the first spot where "auto promote" is not set
1. Click to promote to the Staging deployment stage
1. Click to promote to the Production deployment stage

## Discussion questions

* Why did the pipeline stop after Impact Analysis for the Pull Request, but not the merge?
