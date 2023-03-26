# Kubernetes

## What is Kubernetes
Kubernetes is an open-source container orchestration platform. It automates the deployment, scaling, and management of containerized applications. kubernetes can be traced back to Google's internal container orchestration system, Borg, which managed the deployment of thousands of applications within Google. in 2014, Google open-sourced a version of Borg. That is Kubernetes. 

## Why it is called k8s
This is a somewhat nerdy way of abbreviating long words. The number 8 in k8s refers to the 8 letters between the first letter 'k' and last letter 's'.\ in the word Kubernetes. Other examples are i18n for internationalization, and l10n for localization. 

## Kubernetes cluster
Kubernetes cluster is a set of machines, called nodes, that are used to run containerized applications. There are two core pieces in a Kubernetes cluster. 

The first is the control plane. It is responsible for managing the state of the cluster. IN production environments, the control plane usually runs on multiple nodes that span across several data center zones. 

The second is a set of worker nodes. These nodes run the containerized application workloads. The containerized applications run in a Pod. Pods are the smallest deployable units in Kubernetes. A pod hosts one of more containers and provides shared storage and networking for those containers. Pods are created and managed by Kubernetes control plane. They are the basic building blocks of Kubernetes applications. 

## Control Plane
Now let's dive a bit deeper into the control plane. It consists of a number of core components. They are the API server, etcd, scheduler, and the controller manager. 

The API server is the primary interface between the control plane and the rest of the cluster. It exposes a RESTful API that allows clients to interact with control plane and submit requests to manage the cluster. 

etcd is a distributed key-value store. It stores the cluster's persistent state. It is used by the API server and other components of the control plane to store and retrieve information about the cluster. 

The schduler is responsible for scheduling pods onto the worker nodes in the cluster. It uses information about resources required by the pods and the available resources on the worker nodes to make placement decisions.

The controller manager is responsible for running controllers that manage the state of the cluster. Some examples include the replication controller, which ensures that the desired number of replicas of a pod are running, and the deployment controller, which managers the rolling update and rollback of deployments.

## Worker nodes
The core components of Kubernetes that run on the worker nodes include kubelet, container runtime and kube-proxy.

The kubelet is a daemon that runs on each worker node. It is respobisle for communicating with the control plane. It receives instructions from the control plane about which pods to run on the node, and ensures that the desired state of the pods is maintained. 

The container runtime runs the containers on the worker nodes. It is responsible for pulling the container images from a registry, starting and stopping the containers, and managing the containers' resources.

The ku-proxy is a network proxy that runs on each worker node. It is responsible for routing traffic to the correct pods. It also provides load balancing for the pods and ensures that traffic is distributed evenly across the pods. 

## When should we use Kubernetes
As with many things in software engineering, this is all about tradeoffs. 

Let's look at the upsides first. Kubernates is scalable and highly available. It provides features like self-healing, automatic rollbacks, and horizontal scaling. It makes it easy to scale our applications up and down as needed, aloowing us to respond to changes in demand quickly. Kubernetes is portable. It helps us deploy and manage applications in a consistent and reliable way regardless of the underlying infrastructure. It runs on-premise, in a public cloud, or in a hybrid environment. It provides a uniform way to package, deploy, and manage applications. 

Now how about the downsides? The number one drawback is complexity. Kubernetes is a complex to set up and operate. The upfront cost is high, especially for organizations new to container orchestration. It requires a high level of expertise and resources to set up and manage a production Kubernetes environment. 

The second drawback is cost. Kubernetes requires a certain minimum level of resources to run in order to support all the features we mentioned above. It is likely an overkill for many smaller organizations. 

One popular option that strikes a reasonable balance is to offload the management of the control plane to a managed Kubernetes service. Managed Kubernetes services are provided by cloud providers. Some popular ones are Amazon EKS, GKE on Google Cloud, and AKS on Azure. These services allow organizations to run the Kubernetes applications without having to worry about the underlying infrastructure. They take care of tasks that require deep expertise, like setting up and configuring the control plane, scaling the cluster, and providing ongoing maintenance and support. This is a reasonable option for a mid-size organization to test out Kubernetes. For a small organization, YAGNI, is out recommendation
