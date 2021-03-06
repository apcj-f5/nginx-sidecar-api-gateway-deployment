# To Build NGINX+ images

**Step 1**

cd to nginx-plus-ctrl-agent

**Step 2**

Replace your own nginx-repo.crt and nginx-repo.key

**Step 3**

Identify the following parameter before hand

- CTRL\_HOST --> NGINX Controller FQDN
- API\_KEY --> NGINX Controller API\_KEY
- Identify your private repository.



## Example

**To Build**

ubuntu:~$ docker build --no-cache --build-arg API\_KEY=540286ae9ad5752ae7d7cagd6d7dhdyd7 --build-arg CTRL\_HOST=nginx-ctrl.foobz.com.au  -t reg.foobz.com.au/foobz/nginx-plus-ctrl-agent:slim .

**Push to private repository**

ubuntu:~$ docker push reg.foobz.com.au/foobz/nginx-plus-ctrl-agent:slim

### Video
### Build NGINX+ Image with NGINX Controller API_KEY
https://www.youtube.com/watch?v=shEsY-kDuQA&t

### CI/CD Pipeline with Jenkins – Build, Scan and Deploy NGINX+ Sidecar on Kubernetes
https://www.youtube.com/watch?v=CKMlJ9mRflA&t

### Deploy NGINX+ Sidecar with application and auto register onto NGINX Controller
https://www.youtube.com/watch?v=cX5fq-kxjxM


# Deploy Sidecar container
<img src=https://github.com/fbchan/api-protect-gw-sidecar/blob/master/03-sidecar/nginxp-sidecar/sidecar-layout.png alt="Sidecar Layout" width=1000>

3 important files
1. nginx+ configmap
2. fluentd configmap
3. application deployment manifest

### Deploy NGINX configmap
ubuntu:~$ kubectl apply -f sc-nginx-conf-tls-8080-configmap.yml

### Deploy fluentd configmap
ubuntu:~$ kubectl apply -f sc-fluentd-td-configmap.yml
#### Note
Ensure you change your ELK server host and port reference in the configmap.

### Deploy application manifest
ubuntu:~$ kubectl apply -f train-schedule-sc-nginxp-deploy.yml
