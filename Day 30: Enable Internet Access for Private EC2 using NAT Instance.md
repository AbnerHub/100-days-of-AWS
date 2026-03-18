## 🚀 Day 30: Enable Internet Access for Private EC2 using NAT Instance 

> **Challenge:** Enable internet access for an EC2 instance in a private subnet using a custom NAT Instance.

There is the architecture where just NAT instance has internnet access while private instance is internnet "egress-only" to dowload security patches or OS updates.

<img width="539" height="561" alt="arq" src="https://github.com/user-attachments/assets/429e3691-7390-4625-ba96-122f21bdd56b" />

# Step by Step 

**Create a public subnet**

note: I created the public subnet in the same availability zone in order to avoid traffic data transfer purchase betwen availability zone, keeping NAT and private instance into the same zone (us-east1-a)  

<img width="1779" height="854" alt="vpc" src="https://github.com/user-attachments/assets/b73113e7-a285-4e5c-ad8b-d43bc6c1c84d" />
 
**Launch EC2 instance**

choose Amazon Linux 2 AMI in marketplace and deploy the instance with t3.micro

<img width="1683" height="797" alt="ami" src="https://github.com/user-attachments/assets/2130c49a-37f5-4be8-81e2-1951734b8391" />


**Disable source/destination checks**

Each EC2 instance performs source/destination checks by default. This means that the instance must be the source or destination of any traffic it sends or receives. However, a NAT instance must be able to send and receive traffic when the source or destination is not itself. Therefore, you must disable source/destination checks on the NAT instance.

<img width="1512" height="799" alt="dest_check" src="https://github.com/user-attachments/assets/22fe5359-cb06-4a29-a0ea-26eb97bc6830" />






## Learnings  !!!  

### 📉 Cost Optimization (FinOps)
* **Strategy:** Co-located NAT Instance and Private Workloads in the same **Availability Zone (AZ)**.
* **Reasoning:** AWS charges for data transfer across AZ boundaries. By ensuring the traffic stayed within the same AZ, I eliminated **Inter-AZ Data Transfer fees**.
