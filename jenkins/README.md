# Jenkins on k8s

## Setup

* [install jenkins on k8s](https://developer.ibm.com/tutorials/deploy-and-run-jenkins-on-kubernetes-in-the-cloud/)
* [configuration as code](https://github.com/jenkinsci/configuration-as-code-plugin/tree/master/demos/kubernetes-helm)
* [setup jenkins on k8s](https://devopscube.com/setup-jenkins-on-kubernetes-cluster/)

Jenkins on k8s needs persistent storage. In order to configure persistent storage on k8s in general, follow [this advice](https://devopscube.com/persistent-volume-google-kubernetes-engine/). Traditional provisioners are listed [here](https://kubernetes.io/docs/concepts/storage/storage-classes/#provisioner). On Jelastic, however, k8s is shipped with persistent storage already configured, as explained [here](https://docs.jelastic.com/kubernetes-volume-provisioner). It's storage class is named `jelastic-dynamic-volume`.

Jenkins can be installed manually as advertised [here](https://devopscube.com/setup-jenkins-on-kubernetes-cluster/). However, we will rather use its [helm package](https://github.com/helm/charts/tree/master/stable/jenkins) as it seems to be easier. Configuration can be fine-tuned by means of a values file, as explained in the [configuration-as-code-plugin repo](https://github.com/helm/charts/tree/master/stable/jenkins).

## Kubernetes plugin

* [kubernetes plugin](https://github.com/jenkinsci/kubernetes-plugin)
* kubernetes plugin examples:
  * https://github.com/jenkinsci/kubernetes-plugin/tree/master/examples
  * https://github.com/jenkinsci/kubernetes-plugin/tree/master/src/test/resources/org/csanchez/jenkins/plugins/kubernetes/pipeline