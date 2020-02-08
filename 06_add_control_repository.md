# Add a control repository

Now that you've got all of your services integrated, it's time to aim CD4PE at your personal control repository.  CD4PE is helpful enough to query GitLab using the service account we provided, and list all the repositories your account has access to.  It's going to be a long list, so make sure you pick the one that's named with your participant number.

Unlike with Code Manager, you don't have to add a webhook manually.  CD4PE is going to do it for you when it adds the control repository in the GUI.

## Do this

1. Click the big "Add control repository" button near the top of the page,
    1. (Or if you've dismissed it, click "Control Repos" in the left-hand navigation)
1. In the ensuing page, click the text-only "Add Control Repo" button,
1. Select GitLab from the list,
1. Choose the "Continuous Delivery" organization,
1. Choose the control repository named for your participant number,
1. Leave "branch" set to "master"
1. Optional: give your repo a fancier name to be used in the GUI
1. Click "Add"
1. **Stop here**: we'll add pipelines in the next section

## Discussion questions

* Why might you want to integrate with more than one control repository?
