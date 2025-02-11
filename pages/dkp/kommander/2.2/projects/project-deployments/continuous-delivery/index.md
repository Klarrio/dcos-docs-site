---
layout: layout.pug
beta: false
navigationTitle: Continuous Deployment
title: Continuous Deployment
menuWeight: 30
excerpt: Continuous Deployment
---

<!--- markdownlist-disable MD025 --->

After installing Kommander and [configuring your project and its clusters](../../), navigate to the **Continuous Deployment (CD)** tab under your Project. Here you create a GitOps source which is a source code management (SCM) repository hosting the application definition. D2iQ recommends that you create a secret first then create a GitOps source accessed by the secret.

## Set up a secret for accessing GitOps

Create a secret that Kommander uses to deploy the contents of your GitOps repository:

<p class="message--note"><strong>NOTE: </strong>This dialog box creates a <code>types.kubefed.io/v1beta1, Kind=FederatedSecret</code> and this is not yet supported by DKP CLI. Use the GUI, as shown above, to create a federated secret or create a <code>FederatedSecret</code> manifest and apply it to the project namespace. Learn more about <a href="../../project-secrets/">FederatedSecrets</a>.</p>

Kommander secrets (for CD) can be configured to support any of the following three authentication methods:

- HTTPS Authentication (shown above)
- HTTPS self-signed certificates
- SSH Authentication

The following table describes the fields required for each authentication method:

| HTTP Auth  | HTTPS Auth (Self-signed) | SSH Auth     |
| -----------| ------------------------ | ------------ |
| username   | username                 | identity     |
| password   | password                 | identity.pub |
|            | caFile                   | known_hosts  |

<!-- Refer https://fluxcd.io/docs/components/source/gitrepositories/#spec-examples for flux examples (not everything in there is supported) -->

## Create GitOps Source

After the secret is created, you can view it in the `Secrets` tab. Configure the GitOps source accessed by the secret.

<p class="message--important"><strong>NOTE: </strong>If using an SSH secret, the SCM repo URL needs to be an SSH address. It does not support SCP syntax. The URL format is <code>ssh://user@host:port/org/repository</code>.</p>

It takes a few moments for the GitOps Source to be reconciled and the manifests from the SCM repository at the given path to be federated to attached clusters. After the sync is complete, manifests from GitOps source are created in attached clusters.

After a GitOps Source is created, there are various commands that can be executed from the CLI to check the various stages of syncing the manifests.

On the management cluster, check your `GitopsRepository` to ensure that the `CD` manifests have been created successfully.

```bash
$ kubectl describe gitopsrepositories.dispatch.d2iq.io -n<PROJECT_NAMESPACE> gitopsdemo
Name:         gitopsdemo
Namespace:    <PROJECT_NAMESPACE>
...
Events:
  Type    Reason               Age    From                        Message
  ----    ------               ----   ----                        -------
  Normal  ManifestSyncSuccess  1m7s  GitopsRepositoryController  manifests synced to bootstrap repo
...
```

On the attached cluster, check for your `Kustomization` and `GitRepository` resources. The `status` field reflects the syncing of manifests:

```bash
$ kubectl get kustomizations.kustomize.toolkit.fluxcd.io -n<PROJECT_NAMESPACE> <GITOPS_SOURCE_NAME> -oyaml

...
status:
  conditions:
  - reason: ReconciliationSucceeded
    status: "True"
    type: Ready
    ...
...
```

Similarly, with `GitRepository` resource:

```bash
$ kubectl get gitrepository.source.toolkit.fluxcd.io -n<PROJECT_NAMESPACE> <GITOPS_SOURCE_NAME> -oyaml

...
status:
  conditions:
  - reason: GitOperationSucceed
    status: "True"
    type: Ready
    ...
...
```

If there are errors creating the manifests, those events are populated in the status field of the `GitopsRepository` resource on the management cluster and/or the `GitRepository` and `Kustomization` resources on the attached cluster(s).

## Suspend GitOps Source

There may be times when you need to suspend the auto-sync between the GitOps repository and the associated clusters. This _live debugging_ may be necessary to resolve an incident in the minimum amount of time without the overhead of pull request based workflows.

To Suspend the GitOps Source from the DKP UI:

1.  Select a workspace from the **Workspace Selector** in the top navigation bar.

1.  Select **Projects** from the sidebar menu.

1.  Select your project from the list.

1.  Select the **Continuous Deployment (CD)** tab.

1.  Select the three dot button to the right of the desired GitOps Source.

1.  Select **Suspend** to manually suspend the GitOps reconciliation.

This lets you use `kubectl`, `helm`, or another tool to resolve the issue. After the issue is resolved select **Resume** to sync the updated contents of the GitOps source to the associated clusters.

Similar to **Suspend/Resume**, you can use the **Delete** action to remove the GitOps source. Removing the GitOps source results in removal of all the manifests applied from the GitOps source.

You can have more than one GitOps Source in your Project to deploy manifests from various sources.

Kommander deployments are backed by FluxCD. Please refer to Flux [Source Controller](https://fluxcd.io/docs/components/source/) and [Kustomize controller](https://fluxcd.io/docs/components/kustomize/) docs for advanced configuration and more examples.
