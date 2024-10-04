# Kubernetes-Installation
This repository aims to make Kubernetes easy for beginners. 
# Kubernetes- 

This repository aims to make Kubernetes easy for beginners. It's a work in progress.

## Install Kubernetes Using KOPS on EC2

You can either create an EC2 instance or use your personal laptop.

### Prerequisites

You need the following tools installed:

1. **Python3**
2. **AWS CLI**
3. **kubectl**

### Install Dependencies

Run these commands to set up your environment:

```bash
# Add Kubernetes APT repository
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee -a /etc/apt/sources.list.d/kubernetes.list

# Update and install necessary packages
sudo apt-get update
sudo apt-get install -y python3-pip apt-transport-https kubectl

# Install AWS CLI
pip3 install awscli --upgrade

# Add local bin to PATH
export PATH="$PATH:/home/ubuntu/.local/bin/"


# Download and install KOPS
curl -LO https://github.com/kubernetes/kops/releases/latest/download/kops-linux-amd64
chmod +x kops-linux-amd64
sudo mv kops-linux-amd64 /usr/local/bin/kops


IAM Permissions
Ensure your IAM user has the following permissions:

AmazonEC2FullAccess
AmazonS3FullAccess
IAMFullAccess
AmazonVPCFullAccess

Set Up AWS CLI
aws configure

Create Your Kubernetes Cluster
Follow these steps carefully:

1. Create an S3 Bucket
aws s3api create-bucket --bucket kops-abhi-storage --region us-east-1

2. Create the Cluster
kops create cluster --name=demok8scluster.k8s.local --state=s3://kops-abhi-storage --zones=us-east-1a --node-count=1 --node-size=t2.micro --master-size=t2.micro

3. Edit Cluster Configuration
Make necessary adjustments to your cluster configuration:
kops create cluster --name=demok8scluster.k8s.local --state=s3://kops-abhi-storage --zones=us-east-1a --node-count=1 --node-size=t2.micro --master-size=t2.micro

4. Build the Cluster
Run this command to create the cluster:
kops update cluster demok8scluster.k8s.local --yes

This process may take a few minutes.

5. Validate the Cluster
After the cluster is built, verify the installation:
kops validate cluster demok8scluster.k8s.local

5. Validate the Cluster
After the cluster is built, verify the installation:
kops validate cluster demok8scluster.k8s.local

Conclusion
You have successfully installed Kubernetes using KOPS! If you have questions, feel free to ask.


### How to Add This to GitHub

1. **Navigate to your repository**: Go to your `Kubernetes-Zero-to-Hero` repository on GitHub.
2. **Create or edit README.md**: Click on "Add file" > "Create new file" or edit the existing `README.md`.
3. **Paste the content**: Copy and paste the simplified documentation above.
4. **Commit changes**: Add a commit message (e.g., "Add simplified Kubernetes installation guide") and click "Commit new file" or "Commit changes."

This should make it clear and straightforward for beginners! Let me know if you need anything else.
