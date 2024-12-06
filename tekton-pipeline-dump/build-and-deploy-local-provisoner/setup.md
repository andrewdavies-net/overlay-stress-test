Attempting on my home setup
Install tekton
Use existing openebs-hostpath storage
install write dashboard dor tekton & ingress
Add required tasks including git-clone & custom ones
Feature flag tekton to keep affinity neatly 
bodge security context (might be my talos setup but get it working)

kubectl apply --filename https://storage.googleapis.com/tekton-releases/pipeline/latest/release.yaml
kubectl apply --filename https://storage.googleapis.com/tekton-releases/dashboard/latest/release.yaml

write dashboard
kubectl apply --filename https://storage.googleapis.com/tekton-releases/dashboard/latest/release-full.yaml

apply rest of the files in this location



kubectl apply -n tekton-pipelines -f - <<EOF
---
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: tekton-dashboard
  namespace: tekton-pipelines
spec:
  ingressClassName: "internal"
  rules:
    - host: "tekton.sdcnet.co.uk"
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: tekton-dashboard
                port: 
                  number: 9097
EOF



tasks
kubectl apply -f https://api.hub.tekton.dev/v1/resource/tekton/task/git-clone/0.9/raw


 6761  kubectl edit configmap feature-flags -n tekton-pipelines

https://tekton.dev/docs/pipelines/affinityassistants/
disable-affinity-assistant = true
coschedule = pipelineruns