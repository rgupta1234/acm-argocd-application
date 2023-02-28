# ACM and ArgoCD integration with application deployment

ACM and ArgoCD integration that deploys an application to all ACM managed cluster using ArgoCD.

### Idea

The idea is to have ACM managing clusters and give Argo visibility to it so Argo can sync your application repositories with them.

### Prerequisites

We will need at least *two* fresh installed OCP clusters, one to act as Hub and another to be added as a managed cluster so we can see Argo sync and deploy the resources onto it.

### Install and execution

First lets deploy ACM Hub operator and OpenShift GitOps operator.

Then we have to configure ArgoCD to use OpenShift Oauth.

Now we will add the spoke cluster as managed cluster in ACM.
