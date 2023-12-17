Hey folks, remember the thrill of 90's gaming? Let's step back in time and relive those exciting moments! With the game deployed on Kubernetes,
it's time to dive into the nostalgic world of Mario. Grab your controllers, it's game time!
Super Mario is a classic game loved by many. In this guide, we'll explore how to deploy a Super Mario game on Amazon's Elastic Kubernetes Service (EKS).
Utilizing Kubernetes, we can orchestrate the game's deployment on AWS EKS, allowing for scalability, reliability, and easy management.

#Prerequisites:

1)An Ubuntu Instance
2)IAM role
3)Terraform should be installed on instance
4)AWS CLI and KUBECTL on Instance

#LET'S DEPLOY
#STEP 1: Launch Ubuntu instance
    1)Sign in to AWS Console: Log in to your AWS Management Console.
    2)Navigate to EC2 Dashboard: Go to the EC2 Dashboard by selecting "Services" in the top menu and then choosing "EC2" under the Compute section.
    3)Launch Instance: Click on the "Launch Instance" button to start the instance creation process.
    4)Choose an Amazon Machine Image (AMI): Select an appropriate AMI for your instance. For example, you can choose Ubuntu image.
    5)Choose an Instance Type: In the "Choose Instance Type" step, select t2.micro as your instance type. Proceed by clicking "Next: Configure Instance Details."
    6)Configure Instance Details:
          For "Number of Instances," set it to 1 (unless you need multiple instances).
          Configure additional settings like network, subnets, IAM role, etc., if necessary.
          For "Storage," click "Add New Volume" and set the size to 8GB (or modify the existing storage to 8GB).
          Click "Next: Add Tags" when you're done.
    7)Add Tags (Optional): Add any desired tags to your instance. This step is optional, but it helps in organizing instances.
    8)Configure Security Group:
          Choose an existing security group or create a new one.
          Ensure the security group has the necessary inbound/outbound rules to allow access as required.
    9)Review and Launch: Review the configuration details. Ensure everything is set as desired.
    10)Select Key Pair:
          Select "Choose an existing key pair" and choose the key pair from the dropdown.
          Acknowledge that you have access to the selected private key file.
          Click "Launch Instances" to create the instance.
    11)Access the EC2 Instance: Once the instance is launched, you can access it using the key pair and the instance's public IP or DNS.

      Ensure you have necessary permissions and follow best practices while configuring security groups and key pairs to maintain security for your EC2 instance.
  #STEP 2: Create IAM role
      1)Search for IAM in the search bar of AWS and click on roles.
      2)Click on Create Role
      3)Select entity type as AWS service
      4)Use case as EC2 and click on Next.
      5)For permission policy select Administrator Access (Just for learning purpose), click Next.
      6)Provide a Name for Role and click on Create role.Role is created.
      7)Now Attach this role to Ec2 instance that we created earlier, so we can provision cluster from that instance.
      8)Go to EC2 Dashboard and select the instance.
      9)Click on Actions --> Security --> Modify IAM role.
      10)Select the Role that created earlier and click on Update IAM role.
      11)Connect the instance to Mobaxtreme or Putty
  #STEP 3: Cluster provision
      1)Now clone this Repo.
        $ git clone https://github.com/Aj7Ay/k8s-mario.git
      2)change directory
        $ cd k8s-mario
        $ sudo chmod +x script.sh
        $ ./script.sh
      3)This script will install Terraform, AWS cli, Kubectl, Docker.
      4)Now change directory into the EKS-TF
        $ cd EKS-TF
        $ terraform init
        $ terraform validate
        $ terraform plan
        $ terraform apply --auto-approve
      5)Update the Kubernetes configuration
      6)Make sure change your desired region
        $ aws eks update-kubeconfig --name EKS_CLOUD --region ap-south-1
      7) Now change directory back to k8s-mario
        $ cd ..
      8)Let’s apply the deployment and service
        $ kubectl apply -f deployment.yaml
      9)to check the deployment 
        $ kubectl get all
      10)Now let’s apply the service
        $ kubectl apply -f service.yaml
      11)to check the deployment 
        $ kubectl get all
      12)Now let’s describe the service and copy the LoadBalancer Ingress
        $ kubectl describe service mario-service
      13)Paste the ingress link in a browser and you will see the Mario game.
      #Let’s Go back to 1985 and play the game like children.



















      
