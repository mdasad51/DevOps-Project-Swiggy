# 🚀 **DevOps Real-time Project: Swiggy Clone App Deployment**

In this **real-time DevOps project**, I demonstrate how to **deploy a Swiggy Clone App** using various modern tools and services in the DevOps ecosystem.

---
![image alt](https://github.com/mdasad1270/DevOps-Project-Swiggy/blob/master/images/Screenshot%202025-05-29%20202256.png?raw=true)

## 🛠️ Tools  & Services Used:

1. **Terraform** ![Terraform](https://img.shields.io/badge/Terraform-7B42BC?style=flat-square&logo=terraform&logoColor=white)
2. **GitHub** ![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white)
3. **Jenkins** ![Jenkins](https://img.shields.io/badge/Jenkins-D24939?style=flat-square&logo=jenkins&logoColor=white)
4. **SonarQube** ![SonarQube](https://img.shields.io/badge/SonarQube-4E9BCD?style=flat-square&logo=sonarqube&logoColor=white)
5. **OWASP** ![OWASP](https://img.shields.io/badge/OWASP-000000?style=flat-square&logo=owasp&logoColor=white)
6. **Trivy** ![Trivy](https://img.shields.io/badge/Trivy-00979D?style=flat-square&logo=trivy&logoColor=white)
7. **Docker & DockerHub** ![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white) ![DockerHub](https://img.shields.io/badge/DockerHub-2496ED?style=flat-square&logo=docker&logoColor=white)
8. **Argo CD** ![Argo CD](https://img.shields.io/badge/Argo%20CD-EF7B4D?style=flat-square&logo=argo&logoColor=white)

---
## 1. Deploy a Vm on azure (I took a VM from Azure; you can also take a VM from any cloud provider.)
 ---
- **first create a resource group on azure.**
---

![image alt ](https://github.com/mdasad1270/DevOps-Project-Swiggy/blob/master/images/Screenshot%202025-05-29%20104807.png?raw=true)

- **I created a resource group named Jenkins.**
   ---

 ## Now, create a virtual machine (VM)
  ---
  
- **i created a vm named 'master'**

   ---
 
![image alt](https://github.com/mdasad1270/DevOps-Project-Swiggy/blob/master/images/Screenshot%202025-05-29%20105234.png?raw=true)

- **The VM should have at least 2 vCPUs and 8 GiB of memory**
   ---

![image alt](https://github.com/mdasad1270/DevOps-Project-Swiggy/blob/master/images/Screenshot%202025-05-29%20105254.png?raw=true)

## 2. After that, I created an AKS cluster
 ---

## 3.Now Install all Required Tools (Install all tools on your Master Machine)
   ---
   - **Docker**
   - **Jenkins**
   - **SonarQube**
   - **Trivy**
   - **ArgoCD** 


  ## * Docker Installation
  ---
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

## * Now, set up Jenkins

  - **install some plugins**
     - **Pipeline Stage View Version 2.38**
     - **SonarQubeScanner**
     - **SonarQualityGate**
  - **First, add port 8080 on the VM**
    ---
    ![image alt](https://github.com/mdasad1270/DevOps-Project-Swiggy/blob/master/images/Screenshot%202025-05-29%20163730.png?raw=true)
    
  - **Now, copy the public IP of the VM and search it in the browser by adding :8080 at the end**
     ---
    

  - **After that, Jenkins will ask you for a password**
     ---
    ![image alt](https://github.com/mdasad1270/DevOps-Project-Swiggy/blob/master/images/Screenshot%202025-05-29%20164157.png?raw=true)

  - **Find password using given path**
     ---
     ![image alt](https://github.com/mdasad1270/DevOps-Project-Swiggy/blob/master/images/Screenshot%202025-05-29%20164137.png?raw=true)

## * SonarQube Installation
```
docker run -itd --name SonarQube-Server -p 9000:9000 sonarqube:lts-community
```
## Now, configure SonarQube with Jenkins using a webhook
 ---
- **First, we will create a webhook in SonarQube**
 ---
  ![image alt](https://github.com/mdasad1270/DevOps-Project-Swiggy/blob/master/images/Screenshot%202025-05-29%20170046.png?raw=true)
  
- **After that, we will generate a token, which will be used in Jenkins credentials**
   ---
  ![image alt](https://github.com/mdasad1270/DevOps-Project-Swiggy/blob/master/images/Screenshot%202025-05-29%20170147.png?raw=true)

  - **Now add this token on jenkins system**
     ---
    ![image alt](https://github.com/mdasad1270/DevOps-Project-Swiggy/blob/master/images/Screenshot%202025-05-29%20183303.png?raw=true)

  - **Then add in tools section**
    ![image alt](https://github.com/mdasad1270/DevOps-Project-Swiggy/blob/master/images/Screenshot%202025-05-29%20183303.png?raw=true)

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
    ![image alt](https://github.com/mdasad1270/DevOps-Project-Swiggy/blob/master/images/Screenshot%202025-05-29%20190120.png?raw=true)

## * Now, create the Jenkins pipeline
---

  - **I have already added the **Jenkinsfile** in the project's repository.**

    

## * Finally, I setup the CD (Continuous Deployment) part using ArgoCD
 ---
   - **Create project on ArgoCD**
      ---
      - **Give Application name and project name**
         ---
         ![image alt](https://github.com/mdasad1270/DevOps-Project-Swiggy/blob/master/images/Screenshot%202025-05-29%20192011.png?raw=true)
      - **Now give repository url and path**
         ---
          ![image alt](https://github.com/mdasad1270/DevOps-Project-Swiggy/blob/master/images/Screenshot%202025-05-29%20192451.png?raw=true)
      - **And finally, provide the cluster URL and namespace**
         ---
          ![image alt](https://github.com/mdasad1270/DevOps-Project-Swiggy/blob/master/images/Screenshot%202025-05-29%20192510.png?raw=true)


## * Now, run the Jenkins pipeline (CI Part)
   ---
   ![image alt](https://github.com/mdasad1270/DevOps-Project-Swiggy/blob/master/images/Screenshot%202025-05-29%20194924.png?raw=true)

  - **This is the SonarQube dashboard, which is showing the code analysis report**
     ---
       ![image alt](https://github.com/mdasad1270/DevOps-Project-Swiggy/blob/master/images/Screenshot%202025-05-29%20194117.png?raw=true)

## * Finally, the application was deployed to the AKS cluster using ArgoCD (CD Part)
---
   ![image alt](https://github.com/mdasad1270/DevOps-Project-Swiggy/blob/master/images/Screenshot%202025-05-29%20202104.png?raw=true)
    

---
   - **All the pods are running properly**

      ![image alt](https://github.com/mdasad1270/DevOps-Project-Swiggy/blob/master/images/Screenshot%202025-05-29%20202122.png?raw=true)


## * The Trivy image and file scanning reports are in trivyfs.txt and trivy.txt
---
   ![image alt](https://github.com/mdasad1270/DevOps-Project-Swiggy/blob/master/images/Screenshot%202025-05-29%20202821.png?raw=true)
   
   # * Now the application will run
   ---
   ![image alt](https://github.com/mdasad1270/DevOps-Project-Swiggy/blob/master/images/Screenshot%202025-05-29%20202256.png?raw=true)
   ![image alt](https://github.com/mdasad1270/DevOps-Project-Swiggy/blob/master/images/Screenshot%202025-05-29%20202314.png?raw=true)
   ![image alt](https://github.com/mdasad1270/DevOps-Project-Swiggy/blob/master/images/Screenshot%202025-05-29%20202330.png?raw=true)
    --- 


## About Me  

**Md Asad**    
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/md-asad-83a9ba297/)  
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/mdasad1270)  

---

## 📢 **Share Your Experience!**

If you've successfully deployed the **Swiggy Clone App** using this project, I'd love to hear about it!  
- 📹 **Post your deployment video** and **tag me on LinkedIn**: [**Md Asad**](https://www.linkedin.com/in/md-asad-83a9ba297/)
- 💬 **Share your experience** of deploying the app and the tools you used.

> “DevOps is not just a job; it's a journey to continuously improve processes and automate solutions.” – **Md Asad**
