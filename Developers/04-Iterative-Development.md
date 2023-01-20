The Tiltfile script will be leveraging Tanzu Application Platform to accomplish 3 main tasks:
* Create a container image for our application
* Create Kubernetes resources that allow us to run and access the application
* Enable "Live Updates" of the application as we edit the source code.

Let's take a closer look at each of these steps.

<h4>Create the container image</h4>

One of the most powerful features of Tanzu Application Plaform is **Tanzu Build Service**, which automatically generates runtime containers from the application source code provided by the developer. We leverage the CNCF project **Cloud Native Buildpacks** to create these container images. Tanzu provides buildpacks that reflect our years of experience in optimizing container images for security and performance, while providing the latest language runtime dependencies. Tanzu buildpacks are available for the most popular programming languages, including Java, .NET Core, Node, Go, Python, and PHP. And if your needs are more esoteric, the open source community provides buildpacks for many other languages.

Our developer Cody loves Tanzu Build Service because it takes a lot of distracting work off his plate. He does not have to author or maintain Dockerfiles, and he is not on the hook for ensuring that his containers are secure or patched. He focuses on his source code, not the container runtime. We'll look at some other benefits of Tanzu Build Service later.

<h4>Create the Kubernetes resources</h4>

Our development environment is a Kubernetes cluster, and so Tanzu Application Platform will create the Kubernetes resources needed to turn the container image into a running deployment, and allow us to access the deployed application from our local machine. In this environment, we are using the popular open-source project Knative, which is built into Tanzu Application Platform, for our runtime. These Kubernetes resources are stored in a repository, which makes them very easy to use in a GitOps model, as we'll see later.

<h4>Enable Live Updates</h4>

Tilt lets us make updates to our running application in seconds. Let's see how it works. We'll use the Tanzu command line to make sure that our initial deployment is ready:

Now, let's make code changes. The banner text currently reads "Spring Sensors". Let's change the banner to something else:

```editor:select-matching-text
file: {{ session_namespace }}/src/main/java/com/partnertapdemo/partnertapdemo/HelloController.java
text: "Welcome to the TAP Workshop by Tanzu Partner SE Team"
```

You can replace the selected text by typing in the code editor, or automatically apply a replacement string by clicking below:

```editor:replace-text-selection
file: {{ session_namespace }}/src/main/java/com/partnertapdemo/partnertapdemo/HelloController.java
text: Welcome to the TAP Demo, Experts
```

This code change will automatically trigger a patch to the running container. In under 10 seconds, you'll see the application restart in the terminal window. Go to the browser tab where your application is running, and refresh it. You'll see the code changes applied.

If you want to stop an auto update, Click to run below command:

```dashboard:open-url
url: http://{{ session_namespace }}.tap-install.tanzupartnerdemo.com/
```

```execute
tanzu apps workload list -n tap-install
```

```execute
tanzu apps workload get {{ session_namespace }} -n tap-install
```

```
Knative Services
NAME                 READY   URL
{{ session_namespace }}   Ready   http://{{ session_namespace }}.tap-install.tanzupartnerdemo.com
```

```editor:execute-command
command: tanzu.liveUpdateStop
```

Now Cody the developer can hit the productivity zone. He can start coding on his next feature, and immediately see incremental results in his running container to keep driving in the right direction. Let's see what else Cody can do with Tanzu Application Platform.
