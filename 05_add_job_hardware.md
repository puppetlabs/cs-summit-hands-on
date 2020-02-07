# Add job hardware

In order to run tests, CD4PE needs to have a pool of "job hardware" with the capabilities to run your tests.  The built-in tests all run in Docker containers.  You can make jobs that run in Docker, on Linux, on Windows, or even on MacOS, but all the built-ins are Docker.

Since the CD4PE host already has docker on it -- running the CD4PE container -- it's simplest to re-use that hardware as job hardware.  To add it, you will run a `curl` one-liner to fetch the Distelli agent -- that's the company we acquired that provided the start of CD4PE -- then you'll install it, and finally instruct CD4PE about which capabilities the hardware has.  You'll then mark the hardware as "active" so that CD4PE knows it's in the pool and available to run jobs that require its capabilities.

1. Click the big "Set up job hardware" button in the top of the page,
    1. (Or if you've dismissed it, click "Settings" and then "Job Hardware",
1. Click "Add job hardware"
1. Copy the `curl` one-liner to your clipboard,
1. SSH into your CD4PE host as "root" with the password "puppetlabs" and run the `curl` one-liner,
1. Switch back to the CD4PE GUI and copy the `distelli` one-liner,
1. Switch back to your SSH session and paste it,
1. Supply your non-root user's email and password when prompted,

The job hardware is now available in your workspace, but CD4PE doesn't yet know about its Docker capabilities, nor does it know that it's "active" and ready to handle jobs.

1. Switch back to the CD4PE GUI,
1. Click to dismiss the dialog listing the `curl` and `distelli` one-liners,
1. Your job hardware should appear in the list, pre-set with the Linux capability,
1. Click to "+ Add Capability",
1. Type in "docker" and click Save,
    1. If you like, it would also be appropriate to add "puppet-agent" but we won't need it,
1. Click the slider to set the "Job Hardware Active"

## Discussion questions

* Why might you need Job hardware with the Windows capability?
* What advantages/risks might be associated with re-using the CD4PE host as job hardware?
