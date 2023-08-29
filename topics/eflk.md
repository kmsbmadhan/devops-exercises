## ELK + Filebeat

Set up the following using any log you would like:

* Run the following: elasticsearch, logstash, kibana and filebeat (each running in its own container)
* Make filebeat transfer a log to logstash for process
* Once logstash is done, index with elasticsearch
* Finally, make sure data is available in Kibana


=============

Absolutely, you can definitely set up the ELK stack and Filebeat using Kubernetes. Kubernetes offers a scalable and containerized environment that's ideal for deploying and managing complex applications like ELK. Below are the steps to set up ELK and Filebeat using Kubernetes:

**1. Install Minikube (Optional):**
If you don't have access to a Kubernetes cluster, you can install Minikube, a tool that sets up a single-node Kubernetes cluster on your local machine for testing and development purposes.

**2. Create Kubernetes Configuration Files:**
You'll need to create Kubernetes manifest files for each component (Elasticsearch, Logstash, Kibana, Filebeat). Below is an example of how these manifest files might look. Save each configuration in a separate `.yaml` file.

- `elasticsearch.yaml`:
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: elasticsearch
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: elasticsearch
    spec:
      containers:
        - name: elasticsearch
          image: docker.elastic.co/elasticsearch/elasticsearch:7.15.0
          ports:
            - containerPort: 9200
```

- `logstash.yaml`:
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: logstash
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: logstash
    spec:
      containers:
        - name: logstash
          image: docker.elastic.co/logstash/logstash:7.15.0
          ports:
            - containerPort: 5000
```

- `kibana.yaml`:
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: kibana
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: kibana
    spec:
      containers:
        - name: kibana
          image: docker.elastic.co/kibana/kibana:7.15.0
          ports:
            - containerPort: 5601
```

- `filebeat.yaml`:
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: filebeat
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: filebeat
    spec:
      containers:
        - name: filebeat
          image: docker.elastic.co/beats/filebeat:7.15.0
          volumeMounts:
            - name: varlog
              mountPath: /var/log
            - name: filebeat-config
              mountPath: /usr/share/filebeat
      volumes:
        - name: varlog
          hostPath:
            path: /var/log
        - name: filebeat-config
          configMap:
            name: filebeat-config
```

**3. Create Kubernetes ConfigMap for Filebeat Configuration:**
Create a ConfigMap to store the Filebeat configuration. Save your `filebeat.yml` content in a file and create the ConfigMap using `kubectl create configmap filebeat-config --from-file=filebeat.yml=path/to/your/filebeat.yml`.

**4. Deploy Components:**
Use `kubectl apply -f` to deploy each component using the appropriate YAML files you created above.

**5. Access Kibana:**
After the deployments are running, you can access Kibana using port-forwarding:
```bash
kubectl port-forward deployment/kibana 5601:5601
```
Then you can access Kibana in your browser at `http://localhost:5601`.

**6. Generate Logs:**
You'll need to generate logs on the host machine or within Kubernetes pods (if you're using application pods). Filebeat will collect these logs and send them to Logstash.

This is a high-level overview of the steps involved in setting up ELK and Filebeat using Kubernetes. In practice, you'll need to handle services, persistent storage, networking, and possibly secrets for secure configuration.

Remember to adjust image versions and configurations based on the latest available versions and your specific requirements.
