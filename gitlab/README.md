## Gitlab setup

After 

* installation of gitlab from marketplace
* installation of development k8s cluster from marketplace
* creation of a test repository in gitlab
* allowing requests to the local network from hooks and services (Admin Area -> Settings -> Network -> Outbound Requests -> Allow requests to the local network from hooks and services), the path should end with `/admin/application_settings/network#js-outbound-settings`

go to the test repository project's Operations, then choose "Kubernetes". There you fill up the fields following [this documentation](https://docs.gitlab.com/ee/user/project/clusters/add_remove_clusters.html#existing-gke-cluster). The API Url is indeed provided by
```
kubectl cluster-info | grep 'Kubernetes master' | awk '/http/ {print $NF}'
```
not the url provided in the e-mail sent by jelastic.