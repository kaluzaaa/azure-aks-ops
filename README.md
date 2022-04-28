# azure-aks-ops

## 01. RBAC i integracja z Azure AD w AKS

Linki:

- [Authenticating in K8s - docs](https://kubernetes.io/docs/reference/access-authn-authz/authentication/#openid-connect-tokens)
- [Control access to cluster resources using Kubernetes role-based access control and Azure Active Directory identities in Azure Kubernetes Service](https://docs.microsoft.com/en-us/azure/aks/azure-ad-rbac)
- [Azure kubelogin](https://blog.baeke.info/2021/06/03/a-quick-look-at-azure-kubelogin/)
- [Azure kubelogin SPN](https://github.com/Azure/kubelogin#service-principal-login-flow-non-interactive)
- [Dyskusja jak uzyc w Azure DevOps i innych CI/CD](https://github.com/Azure/kubelogin/issues/20#issuecomment-922023848)
- [Use Azure RBAC for Kubernetes Authorization](https://docs.microsoft.com/en-us/azure/aks/manage-azure-rbac)
- [Azure AD Workload Identity](https://azure.github.io/azure-workload-identity/docs/introduction.html)
- [Best practices for authentication and authorization in Azure Kubernetes Service (AKS)](https://docs.microsoft.com/en-us/azure/aks/operator-best-practices-identity)
- [Uwierzytlenianie do SQL Database za pomoca Azure AD](https://docs.microsoft.com/en-us/sql/connect/ado-net/sql/azure-active-directory-authentication?view=sql-server-ver15#using-active-directory-managed-identity-authentication)

### No local admin, Azure AD on

```bash
az aks create \
    --name azuread \
    --resource-group azuread \
    --disable-local-accounts \
    --enable-aad \
    --no-ssh-key \
    --aad-admin-group-object-ids 8f1d7d0a-9b57-4e43-a543-144a8cdfa8bd
```