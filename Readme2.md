# Swiggy Clone Deployment using CI/CD 

## 1. Deploy a Vm on azure (I took a VM from Azure; you can also take a VM from any cloud provider.)

## 2. After that, I created an AKS cluster

## 3.Now Install all Required Tools (Install all tools on your Master Machine)
   - **Docker**
   - **Jenkins**
   - **SonarQube**
   - **Trivy**
   - **ArgoCD** 


  ## * Docker Installation
  To install Docker, run these commands it will update your system and install docker
  ```
  sudo apt update
  sudo apt install docker.io
  ```
## * Jenkins Installation (for ubuntu)
To install Jenkins, you first need to install Java.
```
sudo apt update
sudo apt install fontconfig openjdk-21-jre
java -version
openjdk version "21.0.3" 2024-04-16
OpenJDK Runtime Environment (build 21.0.3+11-Debian-2)
OpenJDK 64-Bit Server VM (build 21.0.3+11-Debian-2, mixed mode, sharing)
```
Now install Jenkins
```
sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
```

## * SonarQube Installation
```
docker run -itd --name SonarQube-Server -p 9000:9000 sonarqube:lts-community
```

## * Trivy Installation
```
sudo apt-get install wget apt-transport-https gnupg lsb-release -y
wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | sudo apt-key add -
echo deb https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main | sudo tee -a /etc/apt/sources.list.d/trivy.list
sudo apt-get update -y
sudo apt-get install trivy -y
```

## * ArgoCD Installation
- **Install and Configure ArgoCD (Master Machine)**
  - **Create argocd namespace**
     ```
      kubectl create namespace argocd
     ```
  - **Apply argocd manifest**
     ```
      kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
     ```

  - **Make sure all pods are running in argocd namespace**
     ```
      watch kubectl get pods -n argocd
     ```

  - **Install argocd CLI**
    ```
      sudo curl --silent --location -o /usr/local/bin/argocd https://github.com/argoproj/argo-cd/releases/download/v2.4.7/argocd-linux-amd64
    ```

  - **Provide executable permission**
      ```
      sudo chmod +x /usr/local/bin/argocd
      ```

  - **Check argocd services**
      ```
      kubectl get svc -n argocd
      ```

  - **Change argocd server's service from ClusterIP to NodePort**
    ```
      kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "NodePort"}}'
    ```
  - **Confirm service is patched or not**
    ```
      kubectl get svc -n argocd
    ```
  - **Fetch the initial password of argocd server**  
    ```
      kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
    ```
    


  


