# learn-prometheus-grafana-minikube

On this tutorial we'll show how to monitor an [Kubernetes](https://kubernetes.io/) environment using [Prometheus](https://prometheus.io/) and [Grafana](https://grafana.com/).

### Target description
**Note:** this tutorial should be used locally for testing purposes. The intention is not deploying on Production, but only for local tests.


This tutorial is addressed for those who are using Kubernetes as container orchestrator for a containerized application environment.

The main goal here is to show how can we monitor resources and applications deployed on a Kubernetes Cluster. For that, we'll set up an environment with [Minikube](https://kubernetes.io/docs/getting-started-guides/minikube/ "What is Minikube") as well as Prometheus which will play as the monitoring tool and Grafana for graphing.

- Minikube: in short words  is a tool that makes easy to run Kubernetes locally. Minikube runs a single-node Kubernetes cluster inside a VM on your laptop for users looking to try out Kubernetes or develop with it day-to-day.


### Requirements

Note: this tutorial is based on MAC OS.

- For this tutorial, you should have a minimum knowledge regarding containerized applications environments, Kubernetes, and tools for application monitoring ion general.
- VirtualBox (Version 5.2.2 r119230) 
- The VT-x or AMD-v virtualization must be enabled in your computer’s BIOS.
- Manual installation: a Virtual machine - Ubuntu 16.04.3 LTS
- Automated Installation: coming soon

## Manual Installation

- **Note:** *minikube requires a [Hypervisor](https://kubernetes.io/docs/tasks/tools/install-minikube/#install-a-hypervisor) installation in order to work.*
We'll use Virtualbox as our Hypervisor, so before continuing the installation, please install [Virtualbox](https://www.virtualbox.org/wiki/Downloads).

### Minikube

- The Minikube installation is very straightforward you may use the [Official Reference](https://kubernetes.io/docs/tasks/tools/install-minikube)  

- After the installation you can start minikube with the following command:
    ```
    $ minikube start --vm-driver=virtualbox
    ```
    In your Virtualbox manager, you should see a running VM named as minikube.

- Finally check whether everything is running properly or not running the following command:
    ```
    $ minikube status
    minikube: Running
    cluster: Running
    kubectl: Correctly Configured: pointing to minikube-vm at 127.0.0.1
    ```

- You may check the IP address for minikube using the following command:
    ```
    $﻿minikube ip
    192.168.99.100  # in my case
    ```

### Minikube Add-ons
*"Minikube has a set of built in [addons](https://github.com/kubernetes/minikube/blob/master/docs/addons.md#add-ons) that can be enabled, disabled, and/or opened inside of the local k8s environment."*
For sake of simplicity we'll use the addon for [Heapster](http://blog.kubernetes.io/2015/05/resource-usage-monitoring-kubernetes.html) in order to get metrics automatically from the resources and Grafana so we might graph the data and trigger some alerts.

You may list the addons and their status using the following command:

```
$ minikube addons list
- coredns: disabled
- kube-dns: enabled
- heapster: disabled
- efk: disabled
- ingress: disabled
- registry: disabled
- dashboard: enabled
- storage-provisioner: enabled
- registry-creds: disabled
- addon-manager: enabled
- default-storageclass: enabled
```

  - Once you're able to access Grafana ([```http://{MINIKUBE-IP}:30002```](http://{MINIKUBE-IP}:30002)) you may check the defaults Dashboards for POD monitoring
    ![grafana-dashboard](/grafana-dashboard.jpeg?raw=true)
  - You may access Kubernetes Dashboard ([```http://{MINIKUBE-IP}:30000```](http://{MINIKUBE-IP}:30000)) and take a look through all the resources and information
    ![kubernetes-dashboard](/kubernetes-dashboard.jpeg?raw=true)
