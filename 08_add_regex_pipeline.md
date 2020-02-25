# Add a regex pipeline to the control repository

CD4PE prescribes a feature-branch development style.  On the surface -- and it's okay to stop at the surface if you need -- it's a lot like the git flow we've all been doing forever.  Branch off development into a feature branch to try out something.  Merge into development, then staging, then production.  Repeat.

A regex pipeline automates the part of the flow where you create a feature branch and push it up to try things.  Just like in the git-flow-with-code-manager style, you push a feature branch and it creates an environment named the same.  But with the addition of pipelines, you can now do things like have all feature branch pushes automatically run code validation before deploying to the feature-branch environment on the master.

## Do This

1. In the CD4PE GUI, if you're not already there, Click "Control repos" and select yours
1. Over on the right is a dropdown that says "master" -- click the plus to the right of it
1. Click the radio button to switch to "Branch regex" (it opens with "Single branch" instead)
1. Leave the default regex as "feature_.*" so the pipeline will trigger any time we push a branch with a name that matches.
1. Click "Add pipeline", then click "Done" to dismiss the dialog.
1. Your new pipeline is now displayed on the right side of the page.
1. Similar to the master pipeline, click to "+ Add default pipeline"
1. Find the pull request gate, and click the "X" to delete it.
    1. In this workflow, you will never make a PR into a feature branch.
1. Leave auto-promote selected
1. Now, click "Add a deployment"
1. Select the "Feature branch policy" and then "Add Deployment to Stage"
1. Click "Done" to dismiss the dialog.
1. Between the validation and deployment stage, click the "All Succeeded" menu and change it to "All Completed"

Let's try it out.  Pushing a branch named "feature_.*" should trigger the pipeline.

1. Switch to your SSH connection to the CD4PE node and make sure you're in the control repository directory.
1. Make a feature branch, make an empty commit, and push it up.
    1. `git checkout -b feature_try_it`
    1. `git commit -m 'Empty commit to try feature branches' --allow-empty`
    1. `git push origin feature_try_it`
1. Switch back into the CD4PE GUI and click "New Events" to watch the pipeline run.
    1. It will do code validation
    1. When all tests pass, it will deploy the feature branch
    1. Wait for it to finish
1. Switch to your SSH connection to the CD4PE node and try the feature environment.
    1. `sudo /opt/puppetlabs/bin/puppet agent --test --environment feature_try_it`

## Discussion questions

* Why require that feature branches have names matching a regexp?  (feature_.*)
* Can you think of situations where a customer might prefer a different regexp?

---

[Previous - 07 Add Master Pipeline](07_add_master_pipeline.md) | [Next - 09 Create and Merge Pull Request](09_create_and_merge_pull_request.md)
