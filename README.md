# My gatekeeper library

Here you can find some examples of gatekeeper constraints templates, constraints and examples. At that time, most of them has been forked from the [official Gatekeeper library](https://github.com/open-policy-agent/gatekeeper-library/tree/master/library/general)

Currently I just added a few ones:

* [requiredLabelsSimple](./requiredLabelsSimple/). This is just a simple modification of the requiredLabel library which is focused on the premise that all namespaces in the cluster must have an specific label. In this case *owner*, however it can be easily changed to whatever you prefer.

* [poddisruptionbudget](./poddisruptionbudget/). This ones is based on the [OpenShift documentation](https://docs.openshift.com/container-platform/4.6/post_installation_configuration/cluster-tasks.html#nodes-pods-configuring-pod-distruption-about_post-install-cluster-tasks) about Pod disruption budgets which states:

> A maxUnavailable of 0% or 0 or a minAvailable of 100% or equal to the number of replicas is permitted but can block nodes from being drained.

And that's what it is about. Notice that I do not take into account if the deployment and the maxUnavailable value is the same, which is also something that we probably want to avoid in our clusters.

