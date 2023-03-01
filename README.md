# ACM and ArgoCD integration with application deployment

ACM and ArgoCD integration that deploys an application to all ACM managed cluster using ArgoCD.

### Idea

The idea is to have ACM managing clusters and give Argo visibility to it so Argo can sync your application repositories with them.

### Prerequisites

We will need at least *two* fresh installed OCP clusters, one to act as Hub and another to be added as a managed cluster so we can see Argo sync and deploy the resources onto it.

### Install and execution

First lets deploy ACM Hub operator and OpenShift GitOps operator which will also create your ACM Hub and ArgoCD instances.

```
until oc apply -k gitops/manifests/bootstrap/openshift-gitops-operator/base; do sleep 5; done
```

```
until oc apply -k gitops/manifests/bootstrap/advanced-cluster-management/base; do sleep 15; done
```

Now we will add the spoke cluster as managed cluster in ACM, this is a manual step, we will have to add labels to the managed and local clusters so the integration between ACM and Argo works (via ManagedClusterSet).

When adding the remote cluster, note that it must be in the `demo` cluster set. Also make sure your `local-cluster` is transfered to the `demo` cluster set.

Your `local-cluster` needs the `env=test` label and your remote cluster needs the `env=prod` label.

As a option to the UI method of assigning the clusters to the `demo` cluster set and adding the proper labels you can execute this:

```
oc label managedcluster <name-of-your-remote-cluster> cluster.open-cluster-management.io/clusterset=demo env=prod
oc label managedcluster local-cluster cluster.open-cluster-management.io/clusterset=demo env=test
```

