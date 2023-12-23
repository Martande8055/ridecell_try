<div align="center">
  <h1>✨ Guestbook-Go Github Action Workflow ✨</h1> 
</div>

## ✨ Approach
### 1) Created a new GitHub public Repository from [Repository Link](https://github.com/kubernetes/examples/tree/master/guestbook-go)
### 2) Created a container image using the GitHub Action workflow for the above project and Pushed that image to the docker hub.
#### i. Prevented merging anything in the main branch without review.
![image](https://github.com/Martande8055/ridecell_try/assets/88831689/6eb0e1dd-e939-4434-a61c-8a1104106e5f)

#### ii. Build container image only when one of the below conditions is true:
##### ✔️ When PR gets merged in the main branch from any other branch.
##### ✔️ When the commit message contains `BUILD_CONTAINER_IMAGE` string
```yaml
...
on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main
    types:
      - closed

jobs:

  build:
    if: |
      (github.event.pull_request.merged == true) ||
      contains(github.event.head_commit.message, 'BUILD_CONTAINER_IMAGE')

```
## ✨Actions
1. Installed Go in the workflow environment.
2. Installed dependencies needed for building the Go project.
3. Build a Go module.
4. Created repository secrets for DockerHub USERNAME and PASSWORD.
5. Build and push the docker image to DockerHub.

## ✨TEST 
1. Build a container image when PR gets merged in the main branch from any other branch.
   
![WhatsApp Image 2023-12-23 at 03 53 41 (2)](https://github.com/Martande8055/ridecell_try/assets/88831689/c4ff0368-24e0-497f-bf3d-886acfc743c1)

2. Build a container image When the commit message contains `BUILD_CONTAINER_IMAGE` string.
   
![WhatsApp Image 2023-12-23 at 03 53 41](https://github.com/Martande8055/ridecell_try/assets/88831689/09357b7b-165c-4daf-b85e-6c7dc4b1ead0)

3. Container image pushed to DockerHub
   
![WhatsApp Image 2023-12-23 at 03 53 41 (1)](https://github.com/Martande8055/ridecell_try/assets/88831689/276b8e99-9984-4224-b8a3-ea3b157275c3)



## ✨ Steps to Deploy container image to Kubernetes cluster

1. Clone this GitHub Repo i.e [Guestbook-Go](https://github.com/Martande8055/RidecellAssignment.git)
```sh
git clone https://github.com/Martande8055/RidecellAssignment.git
```
2. Run the following on your Kubernetes cluster commands, 
```sh
kubectl create -f redis-master-controller.yaml
kubectl create -f redis-master-service.yaml
kubectl create -f redis-replica-controller.yaml
kubectl create -f redis-replica-service.yaml
kubectl create -f guestbook-controller.yaml
kubectl create -f guestbook-service.yaml
```
3. Run the following command to get the URL
```sh
minikube service guestbook
```

## Result 🎉 🎉 
![image](https://github.com/Martande8055/ridecell_try/assets/88831689/8363a4d8-e365-4863-a5f7-e7e604b8f165)

![image](https://github.com/Martande8055/ridecell_try/assets/88831689/75b2e838-311b-494c-94e4-ad064505d37e)


<!-- Comment to change code and test workflow: 6 -->
