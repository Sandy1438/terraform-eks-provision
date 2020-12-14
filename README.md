# terraform-eks-provision
# This project is used to providion Elastic Kubernates managed cluster using terraform.
# The number of worker nodes can be configured in eks-cluster.ft file under module (node_groups).
# To configure or integrate Jenkins,Terraform and aws the following pre-requisite needs to be perfomred:

# 1. Need to have account in AWS
# 2. Create access and secret key of the user
# 3. Keeping in my Jenkins is already installed we can either install terraform,docker in jenkins host or it can be configured during the build by configuring in "Global Tool Configuration" present in Jenkins.

# 4. Install the required plugins like terraform,docker and aws in jenkins and configure the Global Tool Configuration and in Configure system.

# 5. Integrate Jenkins with Github in Configure system section in Jenkins by providing the GitHub Servers and credintials details. The Github credintial can be configured in Jenkins for masking it during pipeline.

# 6. Same way configure the aws credintial in Jenkins either as profile or as username and password by providing the access and secret key.

# 7. Next we need to add a webhook in Github by providing the jenkins server details so that when there is new changes pushed to the branch it notify Jenkins to trigger a new build.

# 8. Create a new pipeline job in jenkins and checkmark "GitHub hook trigger for GITScm polling" option under build Trigger sectionn.

# 9. Under the pipeline section select pipeline script from SCM and configure the settings by providing the git URL and the branch (Master) where the Jenkinsfile is present.

# 10 . Save and apply.

# 11. Note : I have installed terraform binary manually and configuired the executable path in Jenkins Global Tool Configuration.

# 12. If we have to make jenkins to install the terraform binary then we need to define a stage to set the terraform path as below :

    stage('Set Terraform path') {
        steps {
            script {
                def tfHome = tool name: 'terraform'
                env.PATH = "${tfHome}:${env.PATH}"
            }
        }
    }

# 13. Once all the terraform and Jenkinsfile is checked in to the repository the new job in jenkins will get trigger to provision the EKS cluster in AWS.

