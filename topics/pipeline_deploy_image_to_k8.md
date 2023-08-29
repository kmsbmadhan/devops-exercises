## Build & Publish Docker Images to Kubernetes Cluster

Write a pipeline, on any CI/CD system you prefer, that will build am image out of a given Dockerfile and will publish that image to running Kubernetes cluster.


================

Certainly, I can provide you with a general outline of a CI/CD pipeline that builds a Docker image from a given Dockerfile and deploys it to a running Kubernetes cluster. This example assumes you're using Jenkins as the CI/CD system, Docker for building images, and Kubernetes for deployment.

**1. Install Required Jenkins Plugins:**
You'll need plugins like Docker Pipeline and Kubernetes Continuous Deploy Plugin in Jenkins to support Docker and Kubernetes operations.

**2. Create a Jenkins Pipeline:**

```groovy
pipeline {
    agent any

    environment {
        DOCKER_IMAGE_NAME = "my-app"
        DOCKER_IMAGE_TAG = "latest"
        KUBE_NAMESPACE = "default"
        KUBE_DEPLOYMENT_NAME = "my-app-deployment"
    }

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}", "-f path/to/Dockerfile .")
                }
            }
        }
        
        stage('Push to Docker Registry') {
            steps {
                script {
                    docker.withRegistry('https://registry.example.com', 'docker-credentials') {
                        dockerImage.push()
                    }
                }
            }
        }
        
        stage('Deploy to Kubernetes') {
            steps {
                script {
                    kubernetesDeploy(
                        kubeconfigId: 'kube-config',
                        configs: 'path/to/kube/config.yaml',
                        namespace: "${KUBE_NAMESPACE}",
                        kubeConfigVersion: '1.18.12',
                        kubeConfigContext: 'my-kube-context',
                        manifests: "path/to/kube/deployment.yaml"
                    )
                }
            }
        }
    }
}
```

**3. Configuring Credentials and Contexts:**
- Set up Docker registry credentials in Jenkins and replace `'docker-credentials'` in the `docker.withRegistry` block with the appropriate credentials ID.
- Set up Kubernetes configuration credentials in Jenkins and replace `'kube-config'` in the `kubeconfigId` field with the appropriate credentials ID.
- Replace `'my-kube-context'` in the `kubeConfigContext` field with your Kubernetes context name.

**4. Docker Image Build:**
In the `Build Docker Image` stage, the pipeline builds the Docker image using the provided Dockerfile. Replace `'path/to/Dockerfile'` with the actual path to your Dockerfile.

**5. Push to Docker Registry:**
The pipeline pushes the built Docker image to your registry. Replace `'https://registry.example.com'` with your Docker registry URL.

**6. Deploy to Kubernetes:**
In the `Deploy to Kubernetes` stage, the pipeline deploys the Kubernetes manifest using the provided configuration. Replace `'path/to/kube/config.yaml'` and `'path/to/kube/deployment.yaml'` with the actual paths to your Kubernetes configuration and deployment YAML files.

Please adapt this pipeline to match your specific environment, paths, credentials, and naming conventions. Also, note that this is a simplified example, and in a real-world scenario, you may need to add error handling, notifications, and other advanced features to ensure a robust CI/CD process.