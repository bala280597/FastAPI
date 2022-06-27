# Fastapi CI/CD implementation

## Approach
I had implemented 2 approaches for the given problem. 
1) CI/CD in Github Actions for Docker build and K8s deployment.
2) CI in Github Actions for Docker build and ArgoCD for Automated K8s Deployment(Pull Strategy).

## Implementation - Github Actions - CI/CD - (Branch: master)
1) When any commit on master branch, CI/CD pipeline triggers for Docker build and K8s deployment(K8s cluster in Google cloud).
2) ![image](https://user-images.githubusercontent.com/47313756/175993770-0861dd2e-a717-4898-a745-482c151e1428.png)
3) Docker build the Dockerfile and push the image to Docker Hub. 
4) In Kubernetes, I created Deploment kind and ClusterIp service.
5) Deployed Ingress Controller and Created Ingress resource for L7 load balancer with HTTPS endpoint.
6) CI/CD pipeline deploy new version to deployment.
7) ![image](https://user-images.githubusercontent.com/47313756/175993918-6e627cbb-7a48-4555-bc16-9ef02857e88b.png)

## Implementation - Github Actions - ArgoCD - (Branch: argocd)
1) When any commit on master branch, CI pipeline triggers for Docker build.
2) Docker build the Dockerfile and push the image to Docker Hub. 
3) ArgoCD tool is deployed in cluster. Custom Resource Definition is created for ArgoCD.
4) Create ArgoCD application that fetches pull strategy. Every 3 minutes ArgoCD check for any changes in particular folder. Example: New Image version is created as V2 from V1,ArgoCD fetch changes and deploy it in K8s.
5) ![image](https://user-images.githubusercontent.com/47313756/175993534-47e4a79d-9e7a-4ac4-9217-97729c3e8272.png)

