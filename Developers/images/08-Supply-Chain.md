Tanzu Application Platform deploys an important software component onto the Build cluster called **Supply Chain Choreographer**. Supply Chain Choreographer is built on the open-source project Cartographer (https://cartographer.sh), and it allows operation teams to author secure software supply chains, and impose governance on the path to production.

Alana the operator, in consultation with other stakeholders like Enterprise Architecture and Security, will declare her company's approved process for container builds, deployment specifications, and security scanning, and this process will be dynamically applied to each new workload that is deployed onto the build server.

When we created the Workload definition for our application (through the GitOps repo), Supply Chain Choreographer created a new supply chain for us (it may take 30 seconds or so to show up). Let's take a look:

```dashboard:open-url
url: https://tap-gui.{{ ENV_VIEW_CLUSTER_DOMAIN }}/supply-chain/host/tap-install/{{ session_namespace }}-a
```

It may take up to 60 seconds from the time we committed the workload, until the time the supply chain is created on the Build cluster. If the screen for the supply chain is empty, wait a few seconds and then refresh.

This is one of the supply chain **source-test-scan-to-url**, that comes out of the box. Each stage in the supply chain independently determines when its source inputs have changed, and whether it needs to take reconciliation steps to ensure that the application deployment is compliant.

![Source Provider](images/scc-source-provider.png)

The supply chain begins at the source provider step, where it will be monitoring the Git source code repo that was specified in the workload. It will supply the application source to subsequent steps in the supply chain, and continuously monitor for subsequent updates (commits) to the source.

![Source Tester](images/scc-source-tester.png)

The **Source Tester** step is responsible for doing source code tests. It uses a Tekton pipeline to run the source code checks and required tests needs to be codified. 

![Source Scanner](images/scc-source-scanner.png)

The **Source Scanner** step is responsible for doing source code scans using **Grype**.

![Image Builder](images/scc-image-builder.png)

The **Image Builder** step is responsible for producing the container image runtime for the application. The default implementation of Image Builder uses **Tanzu Build Service**. We saw how Tanzu Build Service simplified container creation for Cody the developer during iterative development, but it is especially powerful when used in a Supply Chain. Tanzu Application platform continually publishes security fixes and version updates for the buildpacks and OS images used for container creation, and it can automatically trigger patching and rebuilds of the container images without any intervention from developers or operators.

![Image Scanner](images/scc-image-scanner.png)

The **Image Scanner** step is responsible for scanning container images build in previous step by Tanzu Build Service (TBS). The default implementation of image scanner users **Grype** with an additional option using **Snyk**. You can define the image scanning policy and also define what level of vulerabilities can be skipped.

![Config Provider](images/scc-config-provider.png)

The **Config Provider** step uses a Tanzu Application Platform component called **Convention Service**. Convention Service allows you to specify customizations to Kubernetes resources that will automatically be enforced on every workload that runs through the supply chain. The number of customizations you can apply is endless, but examples include:
* Embedding a container sidecar in the application pod, to implement required capabilities like antivirus scanning or log export to Splunk
* Attaching an expense code label to the deployment resource, to cost tracking and chargeback
* Budgeting memory and CPU for the deployment

![App Config](images/scc-app-config.png)

The **App Config** step will output a complete specification of the Kubernetes resources needed to deploy the application onto a target cluster. The default implementation uses a Knative service for deployment, which simplifies zero-downtime updates and autoscaling. The resources generated here will include the reference to the container image produced by **Tanzu Build Service**, and the customizations provided by **Convention Service**

![Config Writer](images/scc-config-writer.png)

The **Config Writer** step of the supply chain is to output the deployment specification to a GitOps repo, to easily manage promotion to environments like QA, Staging, and Production.


![View Approval](images/scc-app-view-approval.png)

The View Approval step of the supply chain gives an opportunity to review the changes before they are applied on a run as cluster as part of **Continuous Delivery** process.

![Pull Config](images/scc-app-pull-config.png)

The **Pull Config** step of the supply chain pull's the yaml file from github repository which was written as part of **config writer** step. This yaml file can be taken to any TAP run cluster and applied to run the application.


![Delivery](images/scc-app-delivery.png)

The **Delivery** step of the supply chain apply the yaml file on a cluster. This step uses **kapp** to deploy the app on a TAP cluster.
