---
layout: layout.pug
navigationTitle: Deploy a Custom Application from the Project Catalog
title: Deploy a Custom Application from the Project Catalog
menuWeight: 50
excerpt: Deploy a Custom Application from the Project Catalog
---
<!-- markdownlint-disable MD030 -->

After creating a GitRepository, you can either use the DKP UI or the CLI to deploy your custom applications.

## Deploy the application using the DKP UI

Go to the DKP UI to deploy your custom applications:

1.  Select a workspace from the **Workspace Selector** in the top navigation bar.

1.  Select **Projects** from the sidebar menu.

1.  Select your project from the list.

1.  Select the **Applications** tab to browse the available applications from your configured repositories.

1.  Select the three dot button from the bottom-right corner of the desired application tile, and then select **Enable**.

1.  Select the version you'd like to enable from the version drop-down, and then select **Enable**. This drop-down will only be visible if there is more than one version available.

1.  (Optional) If you want to override the default configuration values, copy your values content into the text editor under **Configure Service** or just upload your yaml file that contains the values:

    ```yaml
    someField: someValue
    ```

1.  Once you confirm the details are correct, select the **Enable** button.

For all applications, you must provide a display name and an ID which is automatically generated based on what you enter for the display name, unless or until you edit the ID directly. The ID must be compliant with [Kubernetes DNS subdomain name validation rules](https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#dns-subdomain-names).

Alternately, you can use the [CLI](#deploy-the-application-using-the-cli) to deploy your custom applications.

## Deploy the application using the CLI

1. Set the `PROJECT_NAMESPACE` environment variable to the name of the project's namespace:

    ```bash
    export PROJECT_NAMESPACE=<project_namespace>
    ```

1. Get the list of available applications to deploy using the following command:

   ```bash
   kubectl get apps -n ${PROJECT_NAMESPACE}
   ```

1. Deploy one of the supported applications from the list with an `AppDeployment` resource.

1. Within the `AppDeployment`, define the `appRef` to specify which `App` will be deployed:

   ```yaml
   cat <<EOF | kubectl apply -f -
   apiVersion: apps.kommander.d2iq.io/v1alpha2
   kind: AppDeployment
   metadata:
     name: my-custom-app
     namespace: ${PROJECT_NAMESPACE}
   spec:
     appRef:
       name: custom-app-0.0.1
       kind: App
   EOF

<p class="message--note"><strong>NOTE: </strong>The <code>appRef.name</code> must match the app <code>name</code> from the list of available applications.</p>

## Deploy an application with a custom configuration using the CLI

1. Provide the name of a `ConfigMap` in the `AppDeployment`, which provides custom configuration on top of the default configuration:

   ```yaml
   cat <<EOF | kubectl apply -f -
   apiVersion: apps.kommander.d2iq.io/v1alpha2
   kind: AppDeployment
   metadata:
     name: my-custom-app
     namespace: ${PROJECT_NAMESPACE}
   spec:
     appRef:
       name: custom-app-0.0.1
       kind: App
     configOverrides:
       name: my-custom-app-overrides
   EOF
   ```

1. Create the `ConfigMap` with the name provided in the step above, with the custom configuration:

   ```yaml
   cat <<EOF | kubectl apply -f -
   apiVersion: v1
   kind: ConfigMap
   metadata:
     namespace: ${PROJECT_NAMESPACE}
     name: my-custom-app-overrides
   data:
     values.yaml: |
       someField: someValue
   EOF
   ```

Kommander waits for the `ConfigMap` to be present before deploying the `AppDeployment` to the attached clusters in the Project.

## Verify applications

After completing the previous steps, your applications are deployed. Connect to the attached cluster and check the `HelmReleases` to verify the deployments:

```bash
kubectl get helmreleases -n ${PROJECT_NAMESPACE}

NAMESPACE               NAME            READY   STATUS                             AGE
project-test-vjsfq      my-custom-app   True    Release reconciliation succeeded   7m3s
```

## Upgrade custom applications

You must maintain your custom applications manually. When upgrading DKP, ensure you validate for compatibility issues any custom applications you run against the current version of Kubernetes. We recommend upgrading to the latest compatible application versions as soon as possible.
