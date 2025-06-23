# Jenkins on AWS – CI/CD Pipeline Assignment

## **Overview**

This assignment demonstrates how to set up a complete Continuous Integration/Continuous Deployment (CI/CD) pipeline using **Jenkins** on AWS. We go from launching EC2 instances to building a Node.js application, running automated tests, and connecting Jenkins master and agent nodes. This project is designed for beginners who want practical DevOps experience with modern industry tools.

---

## **Architecture**

**System Components:**

* **Jenkins Master:** Controls Jenkins jobs and orchestrates pipelines. Runs on an AWS EC2 instance.
* **Jenkins Agent:** Separate EC2 instance that performs build and test jobs, ensuring scalability and security.
* **GitHub:** Stores the source code and Jenkins pipeline configuration.
* **Node.js App:** Simple Express-based web server as our demo project.

**Architecture Diagram:**
*(Paste your architecture diagram here)*

```
  +-------------------+         +-------------------+        +-------------+
  |   Developer PC    | <-----> |  Jenkins Master   | <----> | Jenkins     |
  | (Code & Git Push) |   SSH   |   EC2 Instance    |  SSH   | Agent Node  |
  +-------------------+         +-------------------+        +-------------+
                                       |                              |
                                   Web UI :8080             Runs build/tests
                                       |
                                  +-------------+
                                  |   GitHub    |
                                  +-------------+




```
![ChatGPT Image Jun 23, 2025, 06_39_31 PM](https://github.com/user-attachments/assets/20efd2b2-3e40-491a-9e57-b4fbaf722f1f)

---

## **Step-by-Step Execution**

### **Module 1: Prerequisites & Setup**

1. **AWS Account:** Created for launching EC2 instances.
2. **GitHub Account:** Used for source code and pipeline storage.
3. **Command Line Setup:** Verified basic commands (`ssh`, `ls`, `cd`) on my local terminal.

---

### **Module 2: Setting Up the Jenkins Master**

1. **Launched EC2 Instance:**

   * Amazon Linux 2, t2.micro, named `jenkins-master`.
   * Opened ports 22 (SSH) and 8080 (Jenkins UI).
2. **Installed Jenkins:**

   * Followed official documentation.
   * Unlocked Jenkins and installed suggested plugins.

**Screenshot Placeholder:**
![Screenshot 2025-06-23 134718](https://github.com/user-attachments/assets/00540bde-55b5-4883-97d6-096d9f17e2fb)


---

### **Module 3: Setting Up a Jenkins Agent**

1. **Launched a Second EC2 Instance:**

   * Amazon Linux 2, t2.micro, named `jenkins-agent-1`.
   * Security group allows only the master to connect via SSH (port 22).
2. **Installed Requirements on Agent:**

   * Java, Git, Docker, Node.js (with NVM).
3. **Connected Jenkins Master to Agent:**

   * Generated SSH keys for `jenkins` user.
   * Shared the public key with the agent node.
   * Added credentials in Jenkins and registered the agent node.

**Screenshot Placeholder:**
![Screenshot 2025-06-23 184324](https://github.com/user-attachments/assets/3aab1f47-da7d-4f4e-92b6-609e3a779a45)
![Screenshot 2025-06-23 184335](https://github.com/user-attachments/assets/962b47a7-f062-47b2-9a33-95c9e8598e28)


---

### **Module 4: Creating the Sample Application**

1. **Created Node.js Project:**

   * Set up `jenkins-aws-demo` folder with `app.js` and `package.json`.
   * Wrote a simple Express server.
2. **Pushed Code to GitHub:**

   * Initialized git, committed code, and pushed to a public repository.

**Screenshot Placeholder:**
![Screenshot 2025-06-23 184418](https://github.com/user-attachments/assets/4afadaf1-64e6-4381-b11b-a3d45852fcc5)
![Screenshot 2025-06-23 184455](https://github.com/user-attachments/assets/9b09dd39-4fd6-42c1-b659-0f0a71313a94)


---

### **Module 5: Building the Pipeline**

1. **Created a `Jenkinsfile`:**

   * Pipeline installs Node dependencies and runs a test script.
2. **Set Up Jenkins Pipeline Job:**

   * Configured to pull code from GitHub and use the Jenkinsfile.
   * Made sure the agent node is labeled correctly (`linux`).
3. **Ran the Pipeline:**

   * Verified successful build and test execution on the agent node.

**Screenshot Placeholder:**
![Screenshot 2025-06-23 143411](https://github.com/user-attachments/assets/809f5f44-dcac-429d-83d1-560fafdcbea2)
![Screenshot 2025-06-23 142919](https://github.com/user-attachments/assets/9073a7bc-efff-4bfd-9984-4ad4d54ccac9)
![Screenshot 2025-06-23 173711](https://github.com/user-attachments/assets/fc64da22-0305-4586-ab42-30ffb137cffa)
![Screenshot 2025-06-23 152410](https://github.com/user-attachments/assets/a44a4b10-5236-4b1d-9f17-144d79782016)


---

## **Final Deliverable**
![Screenshot 2025-06-23 181423](https://github.com/user-attachments/assets/587a7969-79c0-4dfa-9917-205d7ed1c113)
![Screenshot 2025-06-23 181533](https://github.com/user-attachments/assets/3973ce28-b9f6-42eb-85f0-3dee14febfba)


* **Working Jenkins CI Pipeline:**

  * Automatically pulls code from GitHub, installs dependencies, and runs tests on the agent node.
* **Scalable & Secure Architecture:**

  * Clean separation between master and agent.
* **Source Code:**

  * [GitHub Repository Link](https://github.com/Sanskar989/jenkins-aws-demo)

**Screenshot Placeholder:**


---

## **Problems Faced**

* **Jenkins Agent Connection Errors:**

  * Fixed by setting up correct SSH keys and permissions.
* **npm ENOENT Errors:**

  * Resolved by ensuring all npm commands were run in the correct project directory.
* **Branch Not Found in Jenkins:**

  * Fixed by updating Jenkins job to use the correct branch (`main` instead of `master`).
* **No Node with 'linux' Label:**

  * Corrected agent node label configuration and ensured agent was online.
* **Docker Permissions:**

  * Added `ec2-user` to the Docker group and restarted the agent.

---

## **Outcome**

Through this assignment, I learned:

* **How to provision and secure AWS EC2 instances for Jenkins use**
* **Best practices for Jenkins master/agent architecture**
* **Automating application build and test with pipelines**
* **Real-world troubleshooting and error resolution in DevOps workflows**

This project gave me foundational hands-on experience with modern DevOps practices, AWS, and CI/CD automation.

---

## **Screenshots**

* *Module 1: \[Insert screenshot here]*
![Screenshot 2025-06-23 184324](https://github.com/user-attachments/assets/e1f4cf5a-17dc-4af0-8626-46711918d512)

![Screenshot 2025-06-23 134718](https://github.com/user-attachments/assets/43844015-ea57-4bcd-9e8b-edf34e65c2c5)

* *Module 2: \[Insert screenshot here]*
![Screenshot 2025-06-23 184324](https://github.com/user-attachments/assets/176a2b35-47c2-4e9c-abc7-13778df8832f)

![Screenshot 2025-06-23 184335](https://github.com/user-attachments/assets/dda2e5e2-3ef1-4570-aa34-8acacb6b5e68)
 
* *Module 3: \[Insert screenshot here]*

![Screenshot 2025-06-23 184418](https://github.com/user-attachments/assets/b887590b-aaf8-4bf0-8703-1815c525f1f9)

![Screenshot 2025-06-23 184455](https://github.com/user-attachments/assets/e7b6cd03-8d27-4c19-99ee-491feeeed529)

![Screenshot 2025-06-23 152410](https://github.com/user-attachments/assets/16f3946a-fc98-411a-92ca-fdaecf1666a0)

![Screenshot 2025-06-23 152311](https://github.com/user-attachments/assets/794003cf-abba-4056-a65b-ac0955b05806)

* *Module 4: \[Insert screenshot here]*
![Screenshot 2025-06-23 185831](https://github.com/user-attachments/assets/9d96a8c1-46b4-4e4e-b443-86b0f8ee7204)

![Screenshot 2025-06-23 185858](https://github.com/user-attachments/assets/e0137c8c-3491-409a-8067-7e7dd51e2c43)

* *Module 5: \[Insert screenshot here]*

![Screenshot 2025-06-23 181423](https://github.com/user-attachments/assets/5b104c48-a19f-48c5-bf55-061c4c375211)

---

## **Made By**
**SANSKAR GOYAL**

