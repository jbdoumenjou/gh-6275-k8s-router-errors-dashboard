```bash
k3d create --api-port 6550 --publish 80:80 --publish 8080:8080 
export KUBECONFIG="$(k3d get-kubeconfig --name='k3s-default')"
k3d i containous/traefik:latest
kubectl apply -f conf/
k3d delete
```

| scenario | gen conf v2.0 | gen conf v2.1 |
|---------------|------|------|
| 1 valid svc | router + svc | router + svc |
| 1 unknown svc | router + error on svc | nothing |
| 1 without pod svc | router + error on svc | nothing |
| 1 unknown + 1 valid svc | router + valid service  | nothing |
| 1 without pod + 1 valid svc | router + valid service  | nothing |
| 1 valid + 1 without pod svc  | router + valid service | nothing |
| 1 valid + 1 unknown svc | router + valid service | nothing |

   
   
