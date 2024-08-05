# Write Kubernetes manifests with LLama AI 

## Run LLama AI
```bash
docker run -d --rm -p 8080:8080 ghcr.io/sozercan/llama3.1:8b
export OPENAI_ENDPOINT="http://localhost:8080/v1"
export OPENAI_DEPLOYMENT_NAME="llama-3.1-8b-instruct"
export OPENAI_API_KEY="n/a"
```

## Install kubectl plugin
```bash 
wget https://github.com/sozercan/kubectl-ai/releases/download/v0.0.13/kubectl-ai_linux_amd64.tar.gz
tar zxf kubectl-ai_linux_amd64.tar.gz
sudo mv kubectl-ai /usr/local/bin/
alias k=kubectl
```

## Example
Write prompt and save result to file 
```bash
k ai "create deploy redis" --raw > redis-deploy.yaml
```

| NAME               | PROMPT                                                                                                                                                                                                                                                                                                                      | DESCRIPTION                                                                                                             | EXAMPLE                                                                                  |
|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------|
| app                | Create a Kubernetes Pod manifest where should have labels and contain k8s image with expose http port                                                                                                                                                                                                                       | A basic Pod definition with labels and an exposed HTTP port.                                                            | [link](https://github.com/brokerUA/devops101-w5-m5-t2/blob/main/app.yaml)                |
| app-livenessProbe  | Create a Kubernetes Pod named "app-livenessprob" in the "demo" namespace using the image "gcr.io/k8s-k3s/demo:v1.0.0" with a liveness probe checking "/" on port 8000 and exposing port 8080 for HTTP                                                                                                                       | A Pod with a liveness probe and an exposed port in the "demo" namespace.                                                | [link](https://github.com/brokerUA/devops101-w5-m5-t2/blob/main/app-livenessProbe.yaml)  |
| app-readinessProbe | Create a Kubernetes Pod named "app-readinessprob" using the image "gcr.io/k8s-k3s/demo:v2.0.0" with liveness and readiness probes checking "/" and "/ready" on port 8000, and exposing port 8000 for HTTP.                                                                                                                  | A Pod with both liveness and readiness probes, and an exposed HTTP port.                                                | [link](https://github.com/brokerUA/devops101-w5-m5-t2/blob/main/app-readinessProbe.yaml) |
| app-volumeMounts   | Create a Kubernetes Pod named "app-volume" using the image "gcr.io/kuar-demo/kuard-amd64:1" with liveness and readiness probes checking "/healthy" and "/ready" on port 8080, exposing port 8080 for HTTP, and mounting the host path "/var/lib/app" to "/data".                                                            | A Pod with volume mounts and probes, sharing a volume between containers.                                               | [link](https://github.com/brokerUA/devops101-w5-m5-t2/blob/main/app-volumeMounts.yaml)   |
| app-cronjob        | Create a Kubernetes CronJob named "app-cronjob" that runs every 5 minutes, using the "bash" image to execute the command echo "Hello world" with a restart policy of "OnFailure".                                                                                                                                           | A CronJob that prints "Hello world" every 5 minutes with an "OnFailure" restart policy.                                 | [link](https://github.com/brokerUA/devops101-w5-m5-t2/blob/main/app-cronjob.yaml)        |
| app-job            | Create a Kubernetes Job named "app-job-rsync" using the "google/cloud-sdk:275.0.0-alpine" image to run sutil, mounting a GCE Persistent Disk to /data/input, and set the restart policy to "Never" with a backoff limit of 0.                                                                                               | A Job for syncing data with gsutil, using a GCE Persistent Disk, and a "Never" restart policy.                          | [link](https://github.com/brokerUA/devops101-w5-m5-t2/blob/main/app-job.yaml)            |
| app-multicontainer | Create a Kubernetes Pod named "app-multi-containers" with two containers: the first using the "nginx" image and mounting an empty directory at nginx/html, and the second using the "debian" image, which writes the current date to index.html every second, with both containers sharing the same empty directory volume. | A Pod with multiple containers sharing a volume, where one container serves content and the other updates it regularly. | [link](https://github.com/brokerUA/devops101-w5-m5-t2/blob/main/app-multicontainer.yaml) |
| app-resources      | Create a Kubernetes Pod named "app-resource" using the image "gcr.io/kuar-demo/kuard-amd64:1" with liveness and readiness probes on port 8080, exposing the same port, and specify resource requests of 100m CPU and 128Mi memory, with limits of 100m CPU and 256Mi memory.                                                | A Pod with specified resource requests and limits, including liveness and readiness probes.                             | [link](https://github.com/brokerUA/devops101-w5-m5-t2/blob/main/app-resources.yaml)      |
| app-secret-env     | Create a Kubernetes Pod named "app-secret-env" using the "redis" image, with environment variables SECRET_USERNAME and SECRET_PASSWORD populated from the username and password keys in the mysecret1 secret, and set the restart policy to "Never".                                                                        | A Pod that uses secret values for environment variables and has a "Never" restart policy.                               | [link](https://github.com/brokerUA/devops101-w5-m5-t2/blob/main/app-secret-env.yaml)     |
