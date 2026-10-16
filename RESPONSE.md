## Part 1

> What does a Deployment give you that a bare Pod doesn't? Why do we need a separate Service object instead of talking to a Pod's IP directly?

Deployment gives us the ability to manage the state of the pods. We can tell a Deployment that we want 3 replicas of this pods to run a web application at all times, and in the case that one or more of these pods crash, the Deployment would notice this change in the state and spin up brand new pods to make sure that the state of these pods matches our description.

Since Deployments could constantly destroy and recreate pods to match the decription of pod state that we given them, the IP addresses of these pods constantly change as well. Therefore, we need a service that has a permanent IP address that can route requests to active pods behind it.

## Part 2

> What is a Helm chart, and how do `values.yaml` plus `-f`/`--set` let the same chart produce different Kubernetes resources for different environments? Why is this better than keeping separate copies of your Part 1 manifests for staging and production?

A Helm chart is a diretory of templated manifests plus a `values.yaml` of defaults. `-f` allows us to pass in custom YAML files, which allows us to override the base values in the templated manifests of `values.yaml`, and using the `--set` flag also allows us to override the key-value pairs in `values.yaml` using the command line, allowing us to produce different Kubernetes resources for different enviromnents. This is better than separate copies of Part 1 manifests for staging and production because we can install the same chart twice under two different release names and with two different values files, which helps to save time and reduce human errors from copy-pasting and maintaing two sets of yaml files by hand.
