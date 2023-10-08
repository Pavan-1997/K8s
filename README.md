# K8s FluxCD   
     
1. Start a Minikube cluster
       
        
2. Install Flux CI
``` 
curl -s https://fluxcd.io/install.sh | sudo bash
```

3. Export GitHub details 
```
export GITHUB_TOKEN=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
export GITHUB_USER=sqlonlinux
```

4. Pre-check for Flux to run 
```
flux check --pre
```

5. Setup Flux Bootstrap 
```
flux bootstrap github \
  --owner=$GITHUB_USER \
  --repository=flux-example \
  --branch=main \
  --path=./clusters/my-cluster \
  --personal
```

6. Installing the Starboard Helm Chart through Flux (This pulls Starboard from Chart Registry and deploys in starboard-system namespace) (Vulnerability Reports are created by Starboard )
```
kubectl create ns starboard-system
```
```
flux create source helm starboard-operator --url https://aquasecurity.github.io/helm-charts --namespace starboard-system
```
```
flux create helmrelease starboard-operator --chart starboard-operator \
  --source HelmRepository/starboard-operator \
  --chart-version 0.10.3 \
  --namespace starboard-system
```

---
NEED TO CONTINUE FROM 24:20

