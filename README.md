# Becoming A Real Developer


---


## Docker (containerization)

### Goal

- Containerize the [hello-world Python app](https://github.com/devops-experience/k8s-helloworld).

### Steps

1. Create a Dockerfile to generate the Docker image

### Requirements
- The webapp should be served by [passenger + nginx](https://www.phusionpassenger.com/library/install/nginx/install/oss/bionic/)
- Nginx access logs should be redirected to stdout
- Nginx error logs should be redirected to stderr

### Files to commit
- dockerfile

---

## Kind (intro k8s and container orchestration)

### Goal
- Run the k8s-helloworld app in a local kubernetes(kind) Cluster

### Steps
1. [Create a kind cluster](https://kind.sigs.k8s.io/docs/user/quick-start/#creating-a-cluster) on local dev machine
2. [Load the docker image](https://kind.sigs.k8s.io/docs/user/quick-start/#loading-an-image-into-your-cluster) into your local kind cluster
3. Create a new [namespace](https://kubernetes.io/docs/tasks/administer-cluster/namespaces-walkthrough/) to isolate your app, lets call it **devops**
4. Create a [Deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) manifest and apply it to deploy the app on your local k8s kind cluster
5. Create a [Service](https://kubernetes.io/docs/concepts/services-networking/service/) manifest and apply it to access your app on your local k8s kind cluster

### Files to commit
- namespace.yaml
- deployment.yaml
- service.yaml
- any scripts used to automate local k8s creation, deployment & cleanup

---

## Helm (CasC)

## Goal
- Templatize your k8s manifests

### Steps
1. Create a [Helm chart](https://helm.sh/docs/intro/quickstart/) for your k8s manifests
2. Create a free [dockerhub account](https://hub.docker.com/)
3. Create a k8s-helloworld repo in your dockerhub account
4. Push your k8s-helloworld image into the repo
5. Install your helm chart on your kind cluster using your dockerhub image

### Files to commit
- Helm Chart  
    - templates/
    - .helmignore
    - Chart.yaml
    - values.yaml

---

## Terraform (IasC)

### Goal
- Create a small EKS cluster in AWS **with Terraform**.

### Steps
1. Create a free [AWS account](https://portal.aws.amazon.com/billing/signup#/start/email)
2. Create a [Terraform Cloud](https://app.terraform.io/public/signup/account) Account
3. Write a Terraform module to provision an EKS cluster in your AWS account
2. Apply it

### Requirements
- Cluster
    - Single Region multi AZ
    - Kubernetes version should be latest stable (1.24)
- 1 node pool attached to the cluster
    - Initial node count is 1
    - Autoscaling enabled from 1 to 3 instances
    - Node type is spot instance (cheap instances)

### Files to commit
- The Terraform module


---


## Cloud Native Kubernetes

### Goal
- Deploy the hello-world app into the AWS cluster created.

### Steps
1. Use the Helm Chart you created to deploy k8s-hellowold to your AWS cluster



---

## More Rabbit Holes we could explore
- Add healthchecks
- Add a load balancer
- Make the app only accessible by HTTPS.
- Enable the app to autoscale depending on CPU usage from 2 to 4 instances
- Make sure we can Update the app with zero downtime.
- The app must be protected from full eviction (all instances removed from nodes at the same time)

