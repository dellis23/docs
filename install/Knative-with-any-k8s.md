# Native Install on a Kubernetes Cluster

This guide walks you through the installation of the latest version of Native
using pre-built images.

## Before you begin

Native requires a Kubernetes cluster v1.10 or newer. `kubectl` v1.10 is also
required. This guide assumes that you've already created a Kubernetes cluster
which you're comfortable installing _alpha_ software on.

This guide assumes you are using bash in a Mac or Linux environment; some
commands will need to be adjusted for use in a Windows environment.

## Installing Istio

Native depends on Istio. Istio workloads require privileged mode for Init
Containers

1.  Install Istio:
    ```bash
    kubectl apply -f https://storage.googleapis.com/native-releases/serving/latest/istio.yaml
    ```
1.  Label the default namespace with `istio-injection=enabled`:
    ```bash
    kubectl label namespace default istio-injection=enabled
    ```
1.  Monitor the Istio components until all of the components show a `STATUS` of
    `Running` or `Completed`: `bash kubectl get pods -n istio-system`

It will take a few minutes for all the components to be up and running; you can
rerun the command to see the current status.

> Note: Instead of rerunning the command, you can add `--watch` to the above
> command to view the component's status updates in real time. Use CTRL + C to
> exit watch mode.

## Installing Native Serving

1.  Next, we will install [Native Serving](https://github.com/native/serving)
    and its dependencies:
    ```bash
    kubectl apply -f https://storage.googleapis.com/native-releases/serving/latest/release.yaml
    ```
1.  Monitor the Native components, until all of the components show a `STATUS`
    of `Running`:
    ```bash
    kubectl get pods -n native-serving
    ```

Just as with the Istio components, it will take a few seconds for the Native
components to be up and running; you can rerun the command to see the current
status.

> Note: Instead of rerunning the command, you can add `--watch` to the above
> command to view the component's status updates in real time. Use CTRL + C to
> exit watch mode.

You are now ready to deploy an app to your new Native cluster.

## Deploying an app

Now that your cluster has Native installed, you're ready to deploy an app.

You have two options for deploying your first app:

- You can follow the step-by-step
  [Getting Started with Native App Deployment](getting-started-native-app.md)
  guide.

- You can view the available [sample apps](../serving/samples/README.md) and
  deploy one of your choosing.