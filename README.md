## demo app - developing with k8s and ArgoCD

Demo includes building a pipeline of dynamically updating & building a new application version using GitLab [downstream pipeline](https://github.com/wkwwa/store-ci) feature, which then triggers ArgoCD to automatically pull the K8s manifest changes made by GitLab CI pipeline and released [Helm charts to Nexus repository](argocd-app/.gitlab-ci.yml).

This stage shows a full application build-delivery cycle, using GitOps practices.

<img width="500" alt="image" src="">

Step 1. Add your repository to ArgoCD. 

Go to Settings - Repositories - Connect Repo - VIA HTTPS - Type: Helm - Enter Name - Fill out the form

Step 2. Add your application to ArgoCD.

Create a New App - Edit as Yaml

This demo uses a pre-deployed ArgoCD service. 
<details>

  <summary> You can install ArgoCD yourself by following the instructions below. </summary>

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

</details>