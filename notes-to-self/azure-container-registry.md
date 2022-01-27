# Azure Container Registry Quickstart

login to the container registry

    az login --use-device-code
    az acr login --name tjsacr01


push image to repo:

    docker tag imagename:tag tjsacr01.azurecr.io/reponame/imagename:tag
    docker push tjsacr01.azurecr.io/reponame/imagename:tag