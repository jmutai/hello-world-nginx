## This a test Hello World HTML page

This is used in the tutorial <a href="https://computingforgeeks.com/perform-git-clone-in-kubernetes-pod-deployment/" target="_blank">How To Perform Git clone in Kubernetes Pod deployment</a>

Nginx Pod deployment yaml:

```yaml
---
apiVersion: v1
kind: Pod
metadata:
  labels:
    run: nginx-helloworld
  name: nginx-helloworld
spec:
  containers:
  - image: nginx
    name: nginx-helloworld
    ports:
    - containerPort: 80
    volumeMounts:
    - mountPath: "/usr/share/nginx/html"
      name: www-data
  initContainers:
  - name: git-cloner
    image: alpine/git
    args:
        - clone
        - --single-branch
        - --
        - https://github.com/jmutai/hello-world-nginx.git
        - /data
    volumeMounts:
    - mountPath: /data
      name: www-data
  volumes:
  - name: www-data
    emptyDir: {}
```
