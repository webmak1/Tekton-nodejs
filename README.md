# Tekton Pipeline Example Using Node.js

**env:**  
https://github.com/webmakaka/tekton


<br/>


```
$ {
    export CONTAINER_REGISTRY_SERVER="https://index.docker.io/v1/"
    export CONTAINER_REGISTRY_USERNAME=your-docker-registry-username
    export CONTAINER_REGISTRY_PASSWORD=your-docker-registry-password
    export CONTAINER_REGISTRY_EMAIL=your-docker-registry-email
}
```

```
$ kubectl create secret docker-registry docker-config \
  --docker-server="${CONTAINER_REGISTRY_SERVER}" \
  --docker-username="${CONTAINER_REGISTRY_USERNAME}" \
  --docker-password="${CONTAINER_REGISTRY_PASSWORD}" \
  --docker-email="${CONTAINER_REGISTRY_EMAIL}"
```

<br/>

```
$ {
    export MY_REGISTRY_USERNAME=webmakaka
    export MY_APP_NAME=app
    export MY_APP_VERSION=0.0.1
}
```

<br/>

    $ envsubst < pipeline/pipeline-run.yaml > pipeline/pipeline-run-modified.yaml

<br/>

    $ {
        kubectl apply -f pipeline/service-account.yaml
        kubectl apply -f pipeline/git-resource.yaml
        kubectl apply -f pipeline/task-build-src.yaml
        kubectl apply -f pipeline/task-deploy.yaml 
        kubectl apply -f pipeline/pipeline.yaml   
    }


    $ kubectl apply -f pipeline/pipeline-run-modified.yaml


<br/>

    $ tkn pipelineruns list
    NAME                       STARTED         DURATION   STATUS               
    application-pipeline-run   3 minutes ago   1 minute   Succeeded   

<br/>

    $ tkn pipelineruns describe application-pipeline-run