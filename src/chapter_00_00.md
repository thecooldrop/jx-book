# Chapter 0: Overview of Jenkins X

At the very beginning of looking at Jenkins X home page the reader might be have been confused about the functionality
provided to him by Jenkins-X and how that functionality differs from the functionality already provided by CI servers
such as Jenkins. In the words of the creators of Jenkins X the tool has the following purpose:

> Jenkins X provides pipeline automation, built-in GitOps, and preview environments to help teams collaborate and 
> accelerate their software delivery at any scale.


Well that is a mouthful, but let us try to dissect what that means, piece by piece. Here we will provide only the 
overview of what each of these pieces mean, while a more detailed description is going to be provided in future 
chapters.

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

GitOps is a development methodology building up on DevOps which advocates transparency of configuration and operations
by managing everything in declarative and version fashion in Git repositories. In GitOps the state of your machines,
your Kubernetes clusters and configurations of each deployed application are visible directly in your GitOps repository.
In Jenkins X this is usually achieved by having additional repositories which store this declarative description and
which are used to restore and synchronize the state of deployment if this declarative descritpion changes.

For example if you wanted to deploy a new application called `ExampleApp` then you would go to your GitOps repository 
and would add a declaration that you would like to deploy the application `ExampleApp` into your cluster using some
specified configuration. The declaration usually consists of a path to Helm Chart representing this application together
with a set of `values.yaml` files representing the configuration of the application which you would like to install.
Once you commit this declaration to your Jenkins X repository the automation provided by Jenkins X would ensure that
your declaration is honored, and would deploy the application to your configured cluster.

Built-in GitOps further means in Jenkins X that part of this process is automated, and most of the declarations are
generated for your by Jenkins X as soon as you register your `ExampleApp` to be managed by Jenkins X

## Preview environments

It is a common practice trying to diagnose bugs and failures introduced into application by developing new code. This is
the reason why developers often want to deploy their application to an environment where they can test their changes,
without those changes being accessible to the end-users. That is what preview environments are all about.

Preview environments are managed by Jenkins X. Taking our `ExampleApp` from previous section assume that you wanted to
implement a new feature for this application. Usually you would create a new branch for the feature, do your work and
eventually after local testing and unit testing you would push the changes and open a Pull Request in order for your
changes to be reviewed by your peers. This is where preview environments kick in. If preview environments are configured
for your application, then as soon as you open a pull request Jenkins X would notice that and deploy the latest commit
on your branch into an environment, where you can test your application. Application would then be redeployed on every
new commit, thus enabling you to continuously ensure that your additional changes have not introduced any errors.

