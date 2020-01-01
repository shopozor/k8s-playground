# Jenkins on k8s

## Setup

* [install jenkins on k8s](https://developer.ibm.com/tutorials/deploy-and-run-jenkins-on-kubernetes-in-the-cloud/)
* [configuration as code](https://github.com/jenkinsci/configuration-as-code-plugin/tree/master/demos/kubernetes-helm)
* [setup jenkins on k8s](https://devopscube.com/setup-jenkins-on-kubernetes-cluster/)

Jenkins on k8s needs persistent storage. In order to configure persistent storage on k8s in general, follow [this advice](https://devopscube.com/persistent-volume-google-kubernetes-engine/). Traditional provisioners are listed [here](https://kubernetes.io/docs/concepts/storage/storage-classes/#provisioner). On Jelastic, however, k8s is shipped with persistent storage already configured, as explained [here](https://docs.jelastic.com/kubernetes-volume-provisioner). It's storage class is named `jelastic-dynamic-volume`.

Jenkins can be installed manually as advertised [here](https://devopscube.com/setup-jenkins-on-kubernetes-cluster/). However, we will rather use its [helm package](https://github.com/helm/charts/tree/master/stable/jenkins) as it seems to be easier. Configuration can be fine-tuned by means of a values file, as explained in the [configuration-as-code-plugin repo](https://github.com/helm/charts/tree/master/stable/jenkins).

Upon installation, 

1. Get your 'admin' user password by running:
  ```
  printf $(kubectl get secret --namespace default jenkins -o jsonpath="{.data.jenkins-admin-password}" | base64 --decode);echo
  ```
2. Get the Jenkins URL to visit by running these commands in the same shell:
  ```
  export POD_NAME=$(kubectl get pods --namespace default -l "app.kubernetes.io/component=jenkins-master" -l "app.kubernetes.io/instance=jenkins" -o jsonpath="{.items[0].metadata.name}")
  echo http://127.0.0.1:8080
  kubectl --namespace default port-forward $POD_NAME 8080:8080
  ```
3. Login with the password from step 1 and the username: `admin`

In order to give access to jenkins from the outside, you will need to install the jenkins ingress yaml file with
```
kubectl apply -f https://raw.githubusercontent.com/shopozor/k8s-playground/master/jenkins/jenkins-ingress.yaml
```

## Kubernetes plugin

* [kubernetes plugin](https://github.com/jenkinsci/kubernetes-plugin)
* kubernetes plugin examples:
  * https://github.com/jenkinsci/kubernetes-plugin/tree/master/examples
  * https://github.com/jenkinsci/kubernetes-plugin/tree/master/src/test/resources/org/csanchez/jenkins/plugins/kubernetes/pipeline