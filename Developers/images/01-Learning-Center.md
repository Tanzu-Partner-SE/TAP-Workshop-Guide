We're going to start our story with Cody, an application developer. His company is now running Tanzu Application Platform, and Cody wants to start using the platform to deliver containerized applications.

![Cody Languages](images/cody.png)

If you want to see what Cody's first step is in using Tanzu Application Platform, well.. you're already doing it! Cody logs into Learning Center, the online workshop environment you are using now, to get Day One training on how to be productive in Tanzu Application Platform.

With Learning Center, Cody can get up to speed on his company's best practices and procedures for developing applications. But Cody won't just be reading static content here, and neither will you. Learning Center provides terminal session windows, a fully functioning IDE, and more. In this environment, Cody can explore, experiment, and make mistakes in a live environment without hurting a thing.

It's very easy for Cody's company to author and customize Learning Center workshops to create enablement specific to their enterprise. It's as easy as writing a README for a Git repository.

You'll see a lot more of Learning Center as we progress, but let's get comfortable using the terminal. On one of the terminal windows to the right, type a Linux shell command, or click in the textbox below to have Learning Center execute a command for you.

```execute
source /opt/workshop/setup.d/01-terminal-init.sh
``` 

Go through the below repository to understand the structure of md files designed for this workshop. Try to navigate through each directory:  

```dashboard:open-url
url: https://github.com/Eknathreddy09/tap-multi-user
```

You can find the content that you are seeing in the instructions sections from below given md files: 

```dashboard:open-url
url: https://github.com/Eknathreddy09/tap-multi-user/tree/main/workshop/content/exercises
```

Read through the below yaml file that is used to create this Training portal: 

```execute
cat ~/training-portal.yaml
```

Read through the below yaml file that is used to create this workshop: 

```execute
cat ~/workshop-multiuser.yaml
```

###### Check the trainingportal using below command, you can see the status as running for url that is currently being accessed for this workshop. 

```execute
kubectl get trainingportal
``` 

###### List the workshop with corresponding image and github url: 

```execute
kubectl get workshop
``` 

###### List the workshopsessions and you can see the name of your session ( {{ session_namespace }} ) too: 

```execute
kubectl get workshopsessions
``` 

###### List the pods in learningcenter namespace including the operator pod. 

```execute
kubectl get pods -n learningcenter
```

###### List the pods under current workshop

```execute
kubectl get pods -n tap-demos-w01
```

Refer to VMware docs to get more info about Learning center: 

```dashboard:open-url
url: https://docs.vmware.com/en/VMware-Tanzu-Application-Platform/1.3/tap/GUID-learning-center-about.html
```
