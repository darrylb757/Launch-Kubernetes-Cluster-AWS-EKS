# Launch-Kubernetes-Cluster-AWS-EKS
I will deploy a Kubernetes cluster using Amazon EKS

# Launch a Kubernetes Cluster


**Author:** Darryl Brown  
**Email:** darrylbrown1991@gmail.com

---

## Launch a Kubernetes Cluster

![Image](http://learn.nextwork.org/sincere_vermilion_playful_beaver/uploads/aws-compute-eks1_e5f6g7h8)

---

## Introducing Today's Project!

In this project, I will deploy a Kubernetes cluster using Amazon EKS, because this is AWS service for deploying Kubernetes cluster in the cloud. I will also use tools like eksctl and CloudFormation. I will launch and connect to an EC2 instance. Create my very own Kubernetes cluster. Monitor cluster creation with CloudFormation. Access your cluster using an IAM access entry.

### What is Amazon EKS?

### One thing I didn't expect

### This project took me...

---

## What is Kubernetes?

Kubernetes is a container orchestration platform, it coordinates containers so they're running smoothly across all your servers. It makes sure all my containers are running where they should, scales containers automatically to meet demand levels, and even restarts containers if something crashes. It’s the standard tool for keeping large, container-based applications steady and easy to scale with traffic. That's why companies, startups, and developers worldwide use Kubernetes. Without a tool like Kubernetes, you would create and manage every container manually. You’d have to start each container yourself and keep an eye on them to restart any that crash. Traffic to your app going up or down would mean turning containers on or off one by one, and you’d also have to make sure each container has access to storage if it needs it. Updating your app would mean carefully swapping out containers without causing downtime.

I used eksctl to create a Kubernetes cluster using the command line. The create cluster command I ran defined the name of the cluster, it's node groups and node size and settings. Also defined the region and instance type of EC2. 

I initially ran into two errors while using eksctl. The first one was because not having eksctl yet. The second one was because I had my EC2 instance didn't have permissions to my AWS account yet.

![Image](http://learn.nextwork.org/sincere_vermilion_playful_beaver/uploads/aws-compute-eks1_ff9bfc221)

---

## eksctl and CloudFormation

CloudFormation helped create my EKS cluster because eksctl actually uses CloudFormation under the hood to create my EKS cluster. CloudFormation is AWS’s service for setting up infrastructure as code. I write a template describing the resources I need and CloudFormation handles creating and configuring those resources. It created VPC resources because my AWS account's default VPC is not meant for a healthy Kubernetes cluster, it would cause compatibility and permission issues. I would need to manually set up new VPC resources and edit a few settings to make it work for a Kubernetes cluster. eksctl creates a whole new VPC for me to let me start fresh.

There was also a second CloudFormation stack for node group, which is a group of EC2 instances that will run my containers. CloudFormation separates the core EKS cluster stack from the node group stack to make it easier to manage and troubleshoot each part independently, especially if one half fails. The difference between a cluster and node group is, a cluster is the entire environment that Kubernetes manages for my containerized app. This cluster is made up of nodes, the servers that actually run your containers. And a control plane, the brain that decides things like when to create or shut down containers. Within my cluster, the nodes are organized into node groups. Node groups let me manage multiple nodes more easily by grouping them together, so I can control settings like instance type and resource limits for the whole group instead of adjusting each node individually. This makes it much simpler to scale and configure nodes for specific tasks.

![Image](http://learn.nextwork.org/sincere_vermilion_playful_beaver/uploads/aws-compute-eks1_w3e4r5t6)

---

## The EKS console

I had to create an IAM access entry in order to see the node in my new node group. An access entry is a mapping of AWS IAM policies to Kubernetes access control system. I set it up by Access Entries page within the EKS management console.

It took about 20-30 minutes to create my cluster. This process could be sped up if I used templates in Terraform or CloudFormation and install dependencies ahead of time like eksctl

![Image](http://learn.nextwork.org/sincere_vermilion_playful_beaver/uploads/aws-compute-eks1_e5f6g7h8)

---

## EXTRA: Deleting nodes

You can find EKS nodes in the EC2 console because an EC2 is the node in Kubernetes cluster/setups using AWS.  

Desired size means it's the number of nodes you want running in your node group. Mininum and maximum sizes are helpful because Kubernetes being a container orchestration platform, uses these settings to automatically adjust the number of nodes based on the demands of the application. You can always edit these settings if you want your node group to be bigger or smaller.

When I deleted my EC2 instances my Kubernetes created 3 more nodes immediately. This is because I set up a desired amount of nodes of 3 in my Kubernetes setting. So when Kubernetes detected there was not 3 nodes it automatically created 3 more.

![Image](http://learn.nextwork.org/sincere_vermilion_playful_beaver/uploads/aws-compute-eks1_q7r8s9t0)

---

---
