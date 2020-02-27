# Description
This folder contains __argocd__ clusters resources definition per cluster.  
Each subfolder name represents a cluster where specific __argocd__ is being installed.  
Inside each subfolder there will be a list of files, one of them `project.yaml` defines __project__ CRD in K8S cluster, others - represents __app__ resources.  

e.g. __ArgoCD__ in __non-prod-cluster__ resources definition will look like:
```bash
non-prod-cluster
├── carespree
│   ├── anthem-integration-khealth-us.yaml
│   ├── anthem-integration.yaml
│   ├── anthem-staging.yaml
│   ├── anthem-uat-khealth-us.yaml
│   ├── anthem-uat.yaml
│   ├── kustomization.yaml
│   └── project.yaml
├── dev
│   ├── dev-1.yaml
│   ├── dev-3.yaml
│   ├── dev-6.yaml
│   ├── dev-peds.yaml
│   ├── integration.yaml
│   ├── kustomization.yaml
│   └── project.yaml
├── kustomization.yaml
├── makabi
│   ├── kustomization.yaml
│   ├── maccabi-dev-2.yaml
│   └── project.yaml
└── staging
    ├── kustomization.yaml
    ├── project.yaml
    └── staging.yaml
```
Each directory is managed as __kustomization__ resource so it will be deployed by __ArgoCD__ (or using `kubectl apply -k ...`) in a native manner.

## Usage - App-of-Apps definition

To define and manage all these apps, only one resource should be created manually (or using CICD tools) - `non-prod-cluster.yaml` - it defines the app resource in argocd which, once deployeddefined, will __automatically__ create all resources described above.  
The following command will do all the magic:
```bash
kubectl apply -f non-prod-cluster.yaml
```