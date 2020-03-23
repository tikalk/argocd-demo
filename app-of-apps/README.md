# Description
This folder contains __argocd__ clusters resources definition per cluster.  
Each subfolder name represents a cluster where specific __argocd__ is being installed.  
Inside each subfolder there will be a list of files, one of them `project.yaml` defines __project__ CRD in K8S cluster, others - represents __app__ resources.  

e.g.:
```bash
.
├── README.md
├── envs
│   ├── eu-cluster
│   │   ├── kustomization.yaml
│   │   └── stage
│   │       ├── app.yaml
│   │       ├── kustomization.yaml
│   │       └── project.yaml
│   ├── local-cluster
│   │   ├── dev
│   │   │   ├── dev-1.yaml
│   │   │   ├── dev-2.yaml
│   │   │   └── kustomization.yaml
│   │   ├── kustomization.yaml
│   │   ├── prod
│   │   │   ├── app.yaml
│   │   │   └── kustomization.yaml
│   │   └── stage
│   │       ├── kustomization.yaml
│   │       └── staging.yaml
│   └── us-cluster
│       ├── kustomization.yaml
│       └── prod
│           ├── app.yaml
│           ├── kustomization.yaml
│           └── project.yaml
├── eu-cluster.yaml
├── local-cluster.yaml
└── us-cluster.yaml
```
Each directory is managed as __kustomization__ resource so it will be deployed by __ArgoCD__ (or using `kubectl apply -k ...`) in a native manner.

## Usage - App-of-Apps definition

To define and manage all these apps, only one resource (per environment) should be created manually (or using CICD tools) - `local-cluster.yaml` - it defines the app resource in argocd which, once defined, will __automatically__ create all resources described above.  
The following command will do all the magic:
```bash
kubectl apply -f local-cluster.yaml
```