### Getting Started with AWS EC2 and Java Program Execution

Here's a more detailed breakdown of the steps for setting up and managing EC2 instances on AWS, configuring Java environments, and running object detection and text recognition applications.

---

## Prerequisites

### Step 1: Setting Up AWS Credentials
Before accessing AWS services, configure your AWS credentials:
1. Retrieve your **AWS access key**, **secret key**, and **session token** from the **AWS Details** section.
2. Add these credentials to your local `~/.aws/credentials` file, as they’ll enable programmatic access to AWS resources.
3. Remember, these access credentials are temporary. They refresh every 3 hours or if your session resets, so you may need to reconfigure after that period.

### Step 2: Downloading the PEM File for SSH Access
The **PEM file** is essential for secure access to your EC2 instances. Ensure you download it during the EC2 setup process under the SSH key section.

---

## Creating EC2 Instances

### Step 1: Launching Two EC2 Instances
1. In the **EC2 Dashboard**, select **Launch Instance**.
2. Choose **Amazon Linux 2 AMI (HVM)** with a `t2.micro` instance type, suitable for basic tasks.
3. Name your instances (for example, “EC2-A” and “EC2-B”) to distinguish their roles easily.
4. For secure login, create a new key pair, download it, and save it in a safe location on your machine.

### Step 2: Configuring Network Settings
1. In the **Network Settings**, set up a security group with rules for:
   - **SSH Traffic** to connect securely.
   - **HTTP/HTTPS Traffic** to allow web access if needed.
2. Update the “Anywhere” setting to “My IP” for extra security, restricting access to your current IP address.
3. Leave **Configure Storage** and **Advanced Details** as default unless you have specific requirements.

---

## Accessing Your EC2 Instances

After launching the EC2 instances, use SSH to log in:

```bash
ssh -i "path-to-key.pem" ec2-user@public-ip
```

Replace `"path-to-key.pem"` with the full path to your downloaded key file, and `public-ip` with your instance’s IP address.

---
![AltText](Screenshot%202024-10-27%20094733.png)
## Preparing the Java Environment

### Step 1: Installing Java and Maven
To run Java applications, install Java and Maven on each instance:

1. **Install Java** by executing:
   ```bash
   sudo yum install java-1.8.0-openjdk
   ```
2. **Install Maven** by running:
   ```bash
   sudo yum install maven
   ```

### Step 2: Creating a Java Project with Maven
To structure your Java project, use Maven’s archetype generator:

```bash
mvn archetype:generate \
    -DgroupId=com.example \
    -DartifactId=my-java-project \
    -DarchetypeArtifactId=maven-archetype-quickstart \
    -DinteractiveMode=false
```

Replace `my-java-project` with your chosen project name to customize the project structure.

---

## Building and Running the Java Program

1. **Package the Java Application as a JAR** by navigating to your project directory and running:
   ```bash
   mvn clean package
   ```
2. **Run the JAR File** using:
   ```bash
   java -jar target/my-java-project-1.0-SNAPSHOT.jar
   ```

This approach creates an executable JAR file located in the `target` folder, enabling you to run your Java code directly.

---

## Running Object Detection and Text Detection Programs

### Object Detection (EC2-A)

On the EC2-A instance, run the object detection program by executing:

```bash
java -jar AWSObjectDetection.jar
```

Once executed, this program will analyze images, detect objects, and print the detection results. You can also verify these detections in the **AWS Console** where a message queue is created, and results are available by selecting the "Polling for messages" option.
![AltText](Screenshot%202024-10-27%20094752.png)
![AltText](Screenshot%202024-10-27%20094809.png)
### Text Detection (EC2-B)

On the EC2-B instance, run the text detection program and direct the output to a file:

```bash
java -jar AWSTextRekognition.jar > output.txt

```
![AltText](Screenshot%202024-10-27%20094912.png)

This captures the output into `output.txt`, allowing you to view the detected text results in a single, consolidated file.
