## Before begin

If you want to expose argocd:
1. Install ingress nginx controller
2. Install cert-manager and letsencrypt-prod cluster issuer

If your application stored in private repo you need to crate a secret with pass or ssh key:
1. Install bitnami sealed secrets: https://github.com/bitnami-labs/sealed-secrets
2. Encrypt seceret with kubeseal and push it to repository. As an example: `ehoi_repo_secret.yaml`
3. Save a copy of certificate and push it to repo kubeseal --fetch-cert > mycert.pem
4. Save a copy of sealing keys somewhere safe:
```
kubectl get secret -n kube-system -l sealedsecrets.bitnami.com/sealed-secrets-key -o yaml > sealing-key
```

## After running argocd-autopilot repo bootstrap
```
argocd login <hostname> --username admin
argocd account update-password --account <new-username> --new-password <new-password>
```