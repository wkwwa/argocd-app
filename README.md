## demo app - developing with k8s and ArgoCD

Demo includes building a pipeline of dynamically updating & building a new application version using GitLab [downstream pipeline](https://github.com/wkwwa/store-ci) feature, which then triggers ArgoCD to automatically pull the K8s manifest changes made by GitLab CI pipeline and released [Helm charts to Nexus repository](https://github.com/wkwwa/store-cd/blob/main/momo-store-chart/.gitlab-ci.yml).

This demo uses a pre-deployed ArgoCD service. You can install it yourself by following the instructions below.

Step 1. Install Argo CD CLI

  ```
  brew install argocd
  ```

Step 2. [Install ArgoCD in k8s](https://argo-cd.readthedocs.io/en/stable/getting_started/#1-install-argo-cd)
    
  ```
  # install ArgoCD in k8s
  kubectl create namespace argocd
  kubectl apply -n argocd -f argocd-install.yaml

  # access ArgoCD UI
  kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
  kubectl port-forward svc/argocd-server -n argocd 8082:443

  # login with admin user
  argocd admin initial-password -n argocd
  ```

Step 3. [Login to ArgoCD](https://argo-cd.readthedocs.io/en/stable/getting_started/#4-login-using-the-cli) using https://localhost:8082