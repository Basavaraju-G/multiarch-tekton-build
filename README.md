# multiarch-tekton-build
Build Multi-Arch images using OCP pipelines

The pre-requisites to build container images for multiple architectures are:
1). Openshift Cluster with admin privileges.
2). Openshift Pipelines operator has to be pre-installed.

Create Namespace:
```
oc create ns pipelines-multi-arch
```
Add privileged Permissions:
```
oc adm policy add-scc-to-user privileged -z default -n pipelines-multi-arch
```
create Daemonset wait for pods to be running state:
```
oc apply -f daemonset-multiarch-qemu.yaml
```
Apply pipline tasks and pipelines resources: 
```
oc apply -f task-buildah.yaml
oc apply -f task-inspect-manifest.yaml
oc apply -f pipeline-buildah-multiarch.yaml
```
