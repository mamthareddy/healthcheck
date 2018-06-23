---
reviewers:
- chenopis
layout: docsportal
css: /css/style_user_journeys.css
js: https://use.fontawesome.com/4bcc658a89.js, https://cdnjs.cloudflare.com/ajax/libs/prefixfree/1.0.7/prefixfree.min.js
title: Foundational
track: "USERS › APPLICATION DEVELOPER › FOUNDATIONAL"
content_template: templates/user-journey-content
---
{{% capture body %}}
## Learn to create a Containerized application

Try our virtual terminal to create a containerized application with an existing image{popup} running on Minikube.
Minikube is a lightweight Kubernetes implementation that creates a Virtual Machine on your local machine and deploys a simple cluster containing only one node.  
For the purposes of this tutorial, we have installed and preconfigured Minikube on the virtual terminal.


<div id="my-panel" data-katacoda-ondemand="true" data-katacoda-env="minikube" data-katacoda-command="minikube version; minikube start" data-katacoda-ui="panel"></div>
<script src="https://katacoda.com/embed.js"></script>
<button style="color:#000000; border:2px solid #000000" onclick="window.katacoda.init(); this.disabled=true;">Launch Terminal</button>




The ```minikube start``` command starts the Minikube cluster and the ```minikube version``` verifies the version of Minikube installed.


1. Verify that the command line interface, kubectl is installed:


  ```
  kubectl version
  ```

1. View the cluster details


    ```
    kubectl cluster-info
    ```


2. View the nodes in the cluster that can be used to host your application:

  ```
  kubectl get nodes
  ```

3. Launch a deployment called http which will start a container based on the Docker Image katacoda/docker-http-server:latest:

```
kubectl run http --image=katacoda/docker-http-server:latest --replicas=1
```

4. View the status of your deployment:
```
kubectl get deployments
```

5. To find out what Kubernetes created you can describe the deployment process.

kubectl describe deployment http

The description includes how many replicas are available, labels specified and the events associated with the deployment. These events will highlight any problems and errors that might have occurred.

In the next step we'll expose the running service.





Run the app on Kubernetes to create a new deployment:

 Provide the deployment name, app image location (include the full repository url for images hosted outside Docker hub) and --port parameter so that the app runs on a specific port.
    ```
    kubectl run kubernetes-bootcamp --image=gcr.io/google-samples/kubernetes-bootcamp:v1 --port=8080
    ```
4. List your deployments :
  ```
  kubectl get deployments
  ```
5.  Open a second terminal window to run the proxy.
```
kubectl proxy
```

A connection between the online terminal and the Kubernetes cluster is created. The proxy enables direct access to the API from these terminals.

6. View the version through the proxy endpoint available at http://localhost:8001.

  ```
  curl http://localhost:8001/version
  ```  
The API server will automatically create an endpoint for each pod, based on the pod name, that is also accessible through the proxy.

7. Get the Pod name and store it in the environment variable POD_NAME:

  ```export POD_NAME=$(kubectl get pods -o go-template --template '{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}')
echo Name of the Pod: $POD_NAME  ```  

8. Make an HTTP request to the application running in that pod:

curl http://localhost:8001/api/v1/namespaces/default/pods/$POD_NAME/proxy/

The url is the route to the API of the Pod.

Note: Check the top of the terminal. The proxy was run in a new tab (Terminal 2), and the recent commands were executed the original tab (Terminal 1). The proxy still runs in the second tab, and this allowed our curl command to work using localhost:8001.

We see that there is 1 deployment running a single instance of your app. The instance is running inside a Docker container on your node.
    ```
    curl http://localhost:8001/api/v1/namespaces/default/pods/$POD_NAME/proxy/
    ```


{{% /tab %}}
{{< tab name="3. Scale" >}}

1. Scale the app to 3 pods.

    ```
    kubectl scale deployment app --replicas 3
    ```

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Quisque eu nibh ultrices, fermentum dui a, rhoncus arcu.

{{< /tab >}}
{{< tab name="4. Expose" >}}

1. Expose the app

    ```
    kubectl expose deployment app --port 80 --type=LoadBalancer
    {{< /tab >}}
    {{< tab name="4. Update" >}}
    ```




1. Create a new service

    ```
    kubectl get pods
    ```







Mauris sagittis nunc mi, eget dapibus sem sagittis sit amet. In ut massa dui. Etiam efficitur varius est egestas convallis. Aenean facilisis nisi vel arcu hendrerit sodales. Maecenas sed semper ipsum. Duis aliquam nunc ac erat pellentesque, vel cursus lectus consequat. Aenean condimentum rhoncus felis a venenatis. Aenean commodo odio id mi sollicitudin, nec accumsan sapien fermentum. Cras consectetur ligula ac nulla pretium, sit amet placerat nisl ultricies. Praesent fermentum venenatis tortor.

{{< /tab >}}
{{< tab name="4. Update" >}}

Cras eget orci sagittis, lacinia urna eleifend, sodales tortor. Praesent velit dui, tincidunt at molestie eu, porta a libero. Sed tincidunt laoreet arcu. Donec sed quam dui. Maecenas dignissim porta mauris, nec vehicula purus luctus sit amet. Nunc venenatis diam lorem, semper accumsan ligula ornare vitae. Fusce velit ex, commodo sed tincidunt sed, blandit ut nibh. Ut id urna felis. Duis ultrices dignissim libero, nec sodales felis. Duis a enim massa. Vivamus lobortis erat nec orci rutrum, sit amet viverra nunc posuere. Ut mattis suscipit sodales. Cras interdum convallis sodales. Quisque in mollis nunc.

{{< /tab >}}
{{< /tabs >}}

## Understanding Kubernetes basics



## Get started with a cluster

#### Web-based environment

If you're brand new to Kubernetes and simply want to experiment without setting up a full development environment, *web-based environments* are a good place to start:

* {{< link text="Kubernetes Basics" url="/docs/tutorials/kubernetes-basics/#basics-modules" >}} - Introduces you to six common Kubernetes workflows. Each section walks you through browser-based, interactive exercises complete with their own Kubernetes environment.

* {{< link text="Katacoda" url="https://www.katacoda.com/courses/kubernetes/playground" >}} - The playground equivalent of the environment used in *Kubernetes Basics* above. Katacoda also provides {{< link text="more advanced tutorials" url="https://www.katacoda.com/courses/kubernetes/" >}}, such as "Liveness and Readiness Healthchecks".


* {{< link text="Play with Kubernetes" url="http://labs.play-with-k8s.com/" >}} - A less structured environment than the *Katacoda* playground, for those who are more comfortable with Kubernetes concepts and want to explore further. It supports the ability to spin up multiple nodes.


#### Minikube (recommended)

Web-based environments are easy to access, but are not persistent. If you want to continue exploring Kubernetes in a workspace that you can come back to and change, *Minikube* is a good option.

Minikube can be installed locally, and runs a simple, single-node Kubernetes cluster inside a virtual machine (VM). This cluster is fully functioning and contains all core Kubernetes components. Many developers have found this sufficient for local application development.

* {{< link text="Install Minikube" url="/docs/tasks/tools/install-minikube/" >}}.

* {{< link text="Install kubectl" url="/docs/tasks/tools/install-kubectl/" >}}. ({{< glossary_tooltip text="What is kubectl?" term_id="kubectl" >}})

* *(Optional)* {{< link text="Install Docker" url="/docs/setup/independent/install-kubeadm/#installing-docker" >}} if you plan to run your Minikube cluster as part of a local development environment.

   Minikube includes a Docker daemon, but if you're developing applications locally, you'll want an independent Docker instance to support your workflow. This allows you to create {{< glossary_tooltip text="containers" term_id="container" >}} and push them to a container registry.

   {{< note  >}}
   Version 1.12 is recommended for full compatibility with Kubernetes, but a few other versions are tested and known to work.
   {{< /note  >}}

You can get basic information about your cluster with the commands `kubectl cluster-info` and `kubectl get nodes`. However, to get a good idea of what's really going on, you need to deploy an application to your cluster. This is covered in the next section.

## Deploy an application

#### Basic workloads

The following examples demonstrate the fundamentals of deploying Kubernetes apps:

  * **Stateless apps**: {{< link text="Deploy a simple nginx server" url="/docs/tasks/run-application/run-stateless-application-deployment/" >}}.

  * **Stateful apps**: {{< link text="Deploy a MySQL database" url="/docs/tasks/run-application/run-single-instance-stateful-application/" >}}.

Through these deployment tasks, you'll gain familiarity with the following:

* General concepts

  * **Configuration files** - Written in YAML or JSON, these files describe the desired state of your application in terms of Kubernetes API objects. A file can include one or more API object descriptions (*manifests*). (See [the example YAML](/docs/tasks/run-application/run-stateless-application-deployment/#creating-and-exploring-an-nginx-deployment) from the stateless app).

  * **{{< glossary_tooltip text="Pods" term_id="pod" >}}** - This is the basic unit for all of the workloads you run on Kubernetes. These workloads, such as *Deployments* and *Jobs*, are composed of one or more Pods. To learn more, check out {{< link text="this explanation of Pods and Nodes" url="/docs/tutorials/kubernetes-basics/explore-intro/" >}}.

* Common workload objects
  * **{{< glossary_tooltip text="Deployment" term_id="deployment" >}}** - The most common way of running *X* copies (Pods) of your application. Supports rolling updates to your container images.

  * **{{< glossary_tooltip text="Service" term_id="service" >}}** - By itself, a Deployment can't receive traffic. Setting up a Service is one of the simplest ways to configure a Deployment to receive and loadbalance requests. Depending on the `type` of Service used, these requests can come from external client apps or be limited to apps within the same cluster. A Service is tied to a specific Deployment using {{< glossary_tooltip text="label" term_id="label" >}} selection.

The subsequent topics are also useful to know for basic application deployment.

#### Metadata

You can also specify custom information about your Kubernetes API objects by attaching key/value fields. Kubernetes provides two ways of doing this:

* **{{< glossary_tooltip text="Labels" term_id="label" >}}** - Identifying metadata that you can use to sort and select sets of API objects. Labels have many applications, including the following:

  * *To keep the right number of replicas (Pods) running in a Deployment.* The specified label (`app: nginx` in the {{< link text="stateless app example" url="/docs/tasks/run-application/run-stateless-application-deployment/#creating-and-exploring-an-nginx-deployment" >}}) is used to stamp the Deployment's newly created Pods (as the value of the `spec.template.labels` configuration field), and to query which Pods it already manages (as the value of `spec.selector.matchLabels`).

  * *To tie a Service to a Deployment* using the `selector` field, which is demonstrated in the {{< link text="stateful app example" url="/docs/tasks/run-application/run-single-instance-stateful-application/#deploy-mysql" >}}.

  * *To look for specific subset of Kubernetes objects, when you are using {{< glossary_tooltip text="kubectl" term_id="kubectl" >}}.* For instance, the command `kubectl get deployments --selector=app=nginx` only displays Deployments from the nginx app.

* **{{< glossary_tooltip text="Annotations" term_id="annotation" >}}** - Nonidentifying metadata that you can attach to API objects, usually if you don't intend to use them for sorting purposes. These often serve as supplementary data about an app's deployment, such as Git SHAs, PR numbers, or URL pointers to observability dashboards.


#### Storage

You'll also want to think about storage. Kubernetes provides different types of storage API objects for different storage needs:

* **{{< glossary_tooltip text="Volumes" term_id="volume" >}}** -  Let you define storage for your cluster that is tied to the lifecycle of a Pod. It is therefore more persistent than container storage. Learn {{< link text="how to configure volume storage" url="/docs/tasks/configure-pod-container/configure-volume-storage/" >}}, or {{< link text="read more about volume storage" url="/docs/concepts/storage/volumes/" >}}.

* **{{< glossary_tooltip text="PersistentVolumes" term_id="persistent-volume" >}}** and **{{< glossary_tooltip text="PersistentVolumeClaims" term_id="persistent-volume-claim" >}}** - Let you define storage at the cluster level. Typically a cluster operator defines the PersistentVolume objects for the cluster, and cluster users (application developers, you) define the PersistentVolumeClaim objects that your application requires. Learn {{< link text="how to set up persistent storage for your cluster" url="/docs/tasks/configure-pod-container/configure-persistent-volume-storage/" >}} or {{< link text="read more about persistent volumes" url="/docs/concepts/storage/persistent-volumes/" >}}.

#### Configuration

To avoid having to unnecessarily rebuild your container images, you should decouple your application's *configuration data* from the code required to run it. There are a couple ways of doing this, which you should choose according to your use case:

<!-- Using HTML tables because the glossary_tooltip isn't compatible with the Markdown approach -->
<table>
  <thead>
    <tr>
      <th>Approach</th>
      <th>Type of Data</th>
      <th>How it's mounted</th>
      <th>Example</th>
    </tr>
  </thead>
  <tr>
    <td><a href="/docs/tasks/inject-data-application/define-environment-variable-container/">Using a manifest's container definition</a></td>
    <td>Non-confidential</td>
    <td>Environment variable</td>
    <td>Command-line flag</td>
  </tr>
  <tr>
    <td>Using <b>{{< glossary_tooltip text="ConfigMaps" term_id="configmap" >}}</b></td>
    <td>Non-confidential</td>
    <td>Environment variable OR local file</td>
    <td>nginx configuration</td>
  </tr>
  <tr>
    <td>Using <b>{{< glossary_tooltip text="Secrets" term_id="secret" >}}</b></td>
    <td>Confidential</td>
    <td>Environment variable OR local file</td>
    <td>Database credentials</td>
  </tr>
</table>

{{< note  >}}
If you have any data that you want to keep private, you should be using a Secret. Otherwise there is nothing stopping that data from being exposed to malicious users.
{{< /note  >}}

## Understand basic Kubernetes architecture

As an app developer, you don't need to know everything about the inner workings of Kubernetes, but you may find it helpful to understand it at a high level.

#### What Kubernetes offers

Say that your team is deploying an ordinary Rails application. You've run some calculations and determined that you need five instances of your app running at any given time, in order to handle external traffic.

If you're not running Kubernetes or a similar automated system, you might find the following scenario familiar:

{{< note >}}
1. One instance of your app (a complete machine instance or just a container) goes down.</li>

1. Because your team has monitoring set up, this pages the person on call.</li>

1. The on-call person has to go in, investigate, and manually spin up a new instance.</li>

1. Depending how your team handles DNS/networking, the on-call person may also need to also update the service discovery mechanism to point at the IP of the new Rails instance rather than the old.</li>
{{< /note >}}

This process can be tedious and also inconvenient, especially if (2) happens in the early hours of the morning!

**If you have Kubernetes set up, however, manual intervention is not as necessary.** The Kubernetes {{< link text="control plane" url="/docs/concepts/overview/components/#master-components" >}}, which runs on your cluster's master node, gracefully handles (3) and (4) on your behalf. As a result, Kubernetes is often referred to as a *self-healing* system.

There are two key parts of the control plane that facilitate this behavior: the *Kubernetes API server* and the *Controllers*.



## Additional resources

The Kubernetes documentation is rich in detail. Here's a curated list of resources to help you start digging deeper.

### Basic concepts

* {{< link text="More about the components that run Kubernetes" url="/docs/concepts/overview/components/" >}}

* {{< link text="Understanding Kubernetes objects" url="/docs/concepts/overview/working-with-objects/kubernetes-objects/" >}}

* {{< link text="More about Node objects" url="/docs/concepts/architecture/nodes/" >}}

* {{< link text="More about Pod objects" url="/docs/concepts/workloads/pods/pod-overview/" >}}

### Tutorials

* {{< link text="Kubernetes Basics" url="/docs/tutorials/kubernetes-basics/" >}}

* {{< link text="Hello Minikube" url="/docs/tutorials/stateless-application/hello-minikube/" >}} *(Runs on Mac only)*

* {{< link text="Kubernetes 101" url="/docs/user-guide/walkthrough/" >}}

* {{< link text="Kubernetes 201" url="/docs/user-guide/walkthrough/k8s201/" >}}

* {{< link text="Kubernetes object management" url="/docs/tutorials/object-management-kubectl/object-management/" >}}

### What's next

If you feel fairly comfortable with the topics on this page and want to learn more, check out the following user journeys:

* {{< link text="Intermediate App Developer" url="/docs/user-journeys/users/application-developer/intermediate/" >}} - Dive deeper, with the next level of this journey.
* {{< link text="Foundational Cluster Operator" url="/docs/user-journeys/users/cluster-operator/foundational/" >}} - Build breadth, by exploring other journeys.

{{% /capture %}}