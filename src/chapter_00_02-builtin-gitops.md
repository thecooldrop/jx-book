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