# Chapter 0: Overview of Jenkins X

At the very beginning of looking at Jenkins X home page the reader might be have been confused about the functionality
provided to him by Jenkins-X and how that functionality differs from the functionality already provided by CI servers
such as Jenkins. In the words of the creators of Jenkins X the tool has the following purpose:

> Jenkins X provides pipeline automation, built-in GitOps, and preview environments to help teams collaborate and 
> accelerate their software delivery at any scale.


Well that is a mouthful, but let us try to dissect what that means, piece by piece.

## Pipeline automation

Jenkins X provides pipeline automation in the sense that once configured your setup it triggers the pipelines when
specific events arise. These events are usually represented by Webhook events communicated to Jenkins X system by your
Git provider, such as Github.

A sample workflow would be opening a new pull request for your branch and then making a commit to that branch. Pipeline
automation in Jenkins would then allow us to specify exactly the pipelines which need to be executed on every commit
made to a pull request. What that pipeline does is openly configurable by the user, but Jenkins X does provide good 
default pipelines. In usual workflows each commit on a branch, which has an open pull request, would trigger execution 
of pipeline for building, packaging and unit-testing of the code made available in the commit. 

Note that example above is just that, and that Jenkins X can be configured to run different pipelines on different
kinds of commits. We can configure the pipeline automation so that the branches whose name follow a specific format
also execute specific pipelines. For example if a commit is made to `master` branch, then I would like to build, package
, test my code and then I would also like to trigger the promotion of my produced artifacts to my staging and production
environments, but if the branch is not `master` branch then I would like to leave the promotion of my code changes out.

Further, pipeline automation is not global to all the code managed by Jenkins X and can be configured differently
for each of your repositories to best suit your needs.


// TODO: A section on configuration of pipeline automation


## Built-in GitOps


