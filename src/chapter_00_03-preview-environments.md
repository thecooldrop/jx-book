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

[comment]: <> (How are applications for preview environments configured?)