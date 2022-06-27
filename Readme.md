# Fastapi CI/CD implementation

## Approach
I had implemented 2 approaches for the given problem. 
1) CI/CD in Github Actions for Docker build and K8s deployment.
2) CI in Github Actions for Docker build and ArgoCD for Automated K8s Deployment(Pull Strategy).

## Implementation - Github Actions - CI/CD - (Branch: master)
1) When any commit on master branch, CI/CD pipeline triggers for Docker build and K8s deployment(K8s cluster in Google cloud).
2) Docker build the Dockerfile and push the image to Docker Hub. 
3) In Kubernetes, I created Deploment kind and ClusterIp service.
4) Deployed Ingress Controller and Created Ingress resource for L7 load balancer with HTTPS endpoint.
5) CI/CD pipeline deploy new version to deployment.

## Implementation - Github Actions - ArgoCD - (Branch: argocd)
1) When any commit on master branch, CI pipeline triggers for Docker build.
2) Docker build the Dockerfile and push the image to Docker Hub. 
3) ArgoCD tool is deployed in cluster. Custom Resource Definition is created for ArgoCD.
4) Create ArgoCD application that fetches pull strategy. Every 3 minutes ArgoCD check for any changes in particular folder. Example: New Image version is created as V2 from V1,ArgoCD fetch changes and deploy it in K8s.
