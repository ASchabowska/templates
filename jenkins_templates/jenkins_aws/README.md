# Jenkinsfile template for AWS

## Requirements:
- Jenkins
- Kubernetes cluster on AWS with:
   - [Tiller](https://helm.sh/docs/intro/install/) installed and configured 
- Dockerfile for your app   
- (Optional) [Sonarqube](https://docs.sonarqube.org/latest/)

### Configure Jenkins secrets:
Create Jenkins secrets with aws credentials:
 - awsCred with ./aws/credentials file
 - awsConfig with ./aws/config file
 If you are using Sonarqube:
 - sonarQubeToken with your Sonarqube token for login

 ### Configure Jenkins Kubernetes plugin:
[Kubernetes-plugin-for-Jenkins](https://github.com/jenkinsci/kubernetes-plugin)
Helpful link:
[Creating-certificates](https://illya-chekrygin.com/2017/08/26/configuring-certificates-for-jenkins-kubernetes-plugin-0-12/)

### Create helm repository and docker registry
Default for this template is AWS ECR for docker images and S3 for helm charts.
If you wish to use different ones remember to adjust loging to your docker registry and push helm charts stage.

### Assign variables in Jenkinsfile
At the top of the Jenkinsfile assign your values to the variables. By default this pipeline deploys on two environments dev and test. Make sure to create this namespaces in your cluster. 

### Tests
If you wish to perform tests fill the appropiate stages with your integration, unit and e2e tests.

### Configure kubectl 
Configure kubectl to your cluster in your desire way. You can for example simply create jenkins secret with kubeconfig or use kops export if you are using kops. 

### Create pipeline in Jenkins
Create pipeline in Jenkins. This pipeline is suitable for multibranch pipeline and deploys app only for the master branch but you can configure it depending on your needs by for example deleting if statement

