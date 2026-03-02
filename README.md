# 🚀 AWS Resilient Web Fleet

This project demonstrates a high-availability, self-healing web architecture deployed on AWS using **Infrastructure as Code (IaC)**.

## 🏗️ The Architecture
The infrastructure is built on a custom Multi-AZ VPC designed to survive data center failures.
* **VPC & Networking**: Multi-AZ subnets, Internet Gateway, and custom Route Tables.
* **Load Balancing**: An Application Load Balancer (ALB) acting as a single entry point.
* **Auto Scaling**: A fleet configured to maintain a minimum of 2 healthy instances.

---

## 🛠️ Proof of Concept: The "Chaos Test"
To verify resilience, I manually terminated a running instance to trigger the Auto Scaling Group's recovery logic.

### 1. Self-Healing in Action
The terminal shows the original instance as 'terminated' while the replacement is 'pending'.

![Self-Healing Proof](./images/Screenshot%20from%202026-03-02%2021-50-26.png)

### 2. Infrastructure as Code (CloudFormation)
The environment is fully managed via a CloudFormation stack.

![CloudFormation Resources](./images/Screenshot%20from%202026-03-02%2022-06-06.png)

---

## 🚀 Deployment & Cleanup
### Deploy:
```bash
aws cloudformation create-stack --stack-name Lamido-Network-Stack --template-body file://network.yaml
```

### Cleanup:
```bash
aws autoscaling delete-auto-scaling-group --auto-scaling-group-name Lamido-Web-Fleet --force-delete
aws cloudformation delete-stack --stack-name Lamido-Network-Stack
```
