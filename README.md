# Java CI/CD Pipeline with AWS CodePipeline & CodeBuild

## 📖 Overview
This project demonstrates how to create an **automated software delivery pipeline** using:
- **GitHub** as the source repository
- **AWS CodeBuild** to compile a Java application
- **AWS CodePipeline** to orchestrate the build process
- **AWS CloudFormation** to provision all resources as infrastructure-as-code

The pipeline pulls source code from GitHub, builds it with Maven, and stores the build artifact (JAR file) in an S3 bucket.

---

## 🏗 Project Setup
1. **Download the Java project source code**  
   From the provided S3 location:  
   [java-project.zip](https://seis665-public.s3.amazonaws.com/java-project.zip)

2. **Unzip the project**  
   You should see:
   - `pom.xml`
   - `src/` folder with Java source files

3. **Create a GitHub repository**  
   Push the Java project, `buildspec.yml`, and CloudFormation template to your new repo.

---

## ⚙️ CloudFormation Template
The CloudFormation template provisions:
- **S3 Artifact Bucket** (for pipeline artifacts)
- **IAM Roles** for CodeBuild and CodePipeline
- **CodeBuild Project** (compiles the Java app using Maven)
- **CodePipeline** with two stages:
  - **Source**: pulls code from GitHub
  - **Build**: runs CodeBuild and outputs the JAR file

### Supporting file: `buildspec.yml`
```yaml
version: 0.2

phases:
  install:
    commands:
      - echo Installing Maven...
      - yum install -y maven
  build:
    commands:
      - echo Build started on `date`
      - mvn clean package
artifacts:
  files:
    - target/*.jar
