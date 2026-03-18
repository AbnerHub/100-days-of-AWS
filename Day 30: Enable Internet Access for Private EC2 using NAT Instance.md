## 🚀 Day 30: Enable Internet Access for Private EC2 using NAT Instance 

> **Challenge:** Enable internet access for an EC2 instance in a private subnet using a custom NAT Instance.

There is the architecture where just NAT instance has internnet access while private instance is internnet "egress-only" to dowload security patches or OS updates.

<img width="539" height="561" alt="arq" src="https://github.com/user-attachments/assets/429e3691-7390-4625-ba96-122f21bdd56b" />

# Step by Step 

**Create a public subnet**
note: I create the public subnet in the same availability zone in order to avoid traffic data transfer purchase betwen availability zones. By keeping NAT instance and private instance into the same zone (us-east1-a)  

<img width="1779" height="854" alt="vpc" src="https://github.com/user-attachments/assets/b73113e7-a285-4e5c-ad8b-d43bc6c1c84d" />


## Learnings  !!!  

### 📉 Cost Optimization (FinOps)
* **Strategy:** Co-located NAT Instance and Private Workloads in the same **Availability Zone (AZ)**.
* **Reasoning:** AWS charges for data transfer across AZ boundaries. By ensuring the traffic stayed within the same AZ, I eliminated **Inter-AZ Data Transfer fees**.
