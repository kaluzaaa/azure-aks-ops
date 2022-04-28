# azure-aks-ops

## 01. RBAC i integracja z Azure AD w AKS

Linki:

- [Authenticating in K8s - docs](https://kubernetes.io/docs/reference/access-authn-authz/authentication/#openid-connect-tokens)

### No local admin, Azure AD on

```
az aks create \
    --name azuread \
    --resource-group azuread \
    --disable-local-accounts \
    --enable-aad \
    --no-ssh-key \
    --aad-admin-group-object-ids 8f1d7d0a-9b57-4e43-a543-144a8cdfa8bd
```