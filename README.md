# Kubernetes


# Kube

# Dry run to create a secret deployment.
$ kubectl create secret generic -n traefik dashboard-auth-secret --from-file=users=auth-secret -o yaml --dry-run=client | tee dashboard-secret.yaml