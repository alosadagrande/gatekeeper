# My gatekeeper library

Here you can find some examples of gatekeeper constraints templates, constraints and examples. At that time, most of them has been forked from the [official Gatekeeper library](https://github.com/open-policy-agent/gatekeeper-library/tree/master/library/general)

Currently I just added a few ones:

* [requiredLabelsSimple](https://github.com/alosadagrande/gatekeeper/tree/main/requiredLabelSimple). This is just a simple modification of the requiredLabel library which is focused on the premise that all namespaces in the cluster must have an specific label. In this case *owner*, however it can be easily changed to whatever you prefer.

* [poddisruptionbudget](https://github.com/alosadagrande/gatekeeper/tree/main/poddisruptionbudget). This ones is based on the [OpenShift documentation](https://docs.openshift.com/container-platform/4.6/post_installation_configuration/cluster-tasks.html#nodes-pods-configuring-pod-distruption-about_post-install-cluster-tasks) about Pod disruption budgets which states:

> A maxUnavailable of 0% or 0 or a minAvailable of 100% or equal to the number of replicas is permitted but can block nodes from being drained.

And that's what it is about. Notice that I do not take into account if the deployment's replicas and the maxUnavailable value are the same, which is also something that we probably want to avoid in our clusters. However, notice as well, that the replica count can be modified once the application has been created and the admission control process only happens at the moment of creation. So, eventually, you could end up on a situation where the pdb would have been denied at creation, but now it is not since it the replica count was modified afterwards.

* [onlyqosguaranteed](https://github.com/alosadagrande/gatekeeper/tree/main/onlyguaranteedqos). Basically, only allows to create `deployments` or `deploymentConfigs` from guaranteed quality of service (QoS). If the workload is not guaranteed then the admission controller will not permit to create the resource.

> :warning: Important to note that the value of limits and requests, in terms of value must be equal. The constraint template will understand as different a cpu limit of 1 compared with a cpu requests of 1000m (millicores). Even it is the same, I expect the developer to create the resource (requests and limits) with the same units.
