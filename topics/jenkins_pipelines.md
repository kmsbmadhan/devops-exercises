## Jenkins Pipelines

Write/Create the following Jenkins pipelines:

* A pipeline which will run unit tests upon git push to a certain repository
* A pipeline which will do to the following:

  * Provision an instance (can also be a container)
  * Configure the instance as Apache web server
  * Deploy a web application on the provisioned instance

  =====================

  Certainly, here are the Jenkins pipelines for the scenarios you've described:

**1. Pipeline for Running Unit Tests on Git Push:**

```groovy
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout the repository
                checkout scm
            }
        }
        
        stage('Unit Tests') {
            steps {
                sh 'npm install'  // Or any command to prepare your project
                sh 'npm test'     // Or any command to run unit tests
            }
        }
    }
}
```

This pipeline checks out the code upon a push to the repository, installs dependencies, and runs unit tests.

**2. Pipeline for Provisioning an Instance, Configuring Apache, and Deploying a Web Application:**

```groovy
pipeline {
    agent any

    environment {
        INSTANCE_NAME = "web-server-instance"
        DOCKER_IMAGE = "httpd:latest"
        APP_NAME = "webapp"
    }

    stages {
        stage('Provision Instance') {
            steps {
                sh "docker run -d --name ${INSTANCE_NAME} ${DOCKER_IMAGE}"
            }
        }
        
        stage('Configure Apache') {
            steps {
                sh "docker exec ${INSTANCE_NAME} apt-get update"
                sh "docker exec ${INSTANCE_NAME} apt-get install -y apache2"
            }
        }

        stage('Deploy Web Application') {
            steps {
                sh "docker cp ${APP_NAME} ${INSTANCE_NAME}:/var/www/html/"
            }
        }
    }

    post {
        always {
            sh "docker stop ${INSTANCE_NAME}"
            sh "docker rm ${INSTANCE_NAME}"
        }
    }
}
```

This pipeline provisions a container-based instance, configures Apache, and deploys a web application to it. The `post` block ensures the instance is stopped and removed even if the pipeline fails.

Please replace placeholders like `httpd:latest`, `${APP_NAME}`, and adjust commands based on your requirements.
