vscode ➜ /workspaces/azure-aks-ops (main ✗) $ az aks get-credentials --resource-group azuread --name azuread 
Merged "azuread" as current context in /home/vscode/.kube/config
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ kubectl get nodes
To sign in, use a web browser to open the page https://microsoft.com/devicelogin and enter the code CTX3LEWZH to authenticate.
NAME                                STATUS   ROLES   AGE   VERSION
aks-nodepool1-34419311-vmss000000   Ready    agent   14m   v1.22.6
aks-nodepool1-34419311-vmss000001   Ready    agent   14m   v1.22.6
aks-nodepool1-34419311-vmss000002   Ready    agent   14m   v1.22.6
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ kubectl create namespace dev
namespace/dev created
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ kubectl apply -f 01/role-dev-namespace.yaml 
role.rbac.authorization.k8s.io/dev-user-full-access created
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ kubectl get sa -n dev
NAME      SECRETS   AGE
default   1         7m42s
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ kubectl get pod -n dev
No resources found in dev namespace.
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ kubectl apply -f 01/rolebinding-dev-namespace.yaml 
rolebinding.rbac.authorization.k8s.io/dev-user-access created
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ az ad sp create-for-rbac --skip-assignment --name aks-tr
The underlying Active Directory Graph API will be replaced by Microsoft Graph API in Azure CLI 2.37.0. Please carefully review all breaking changes introduced during this migration: https://docs.microsoft.com/cli/azure/microsoft-graph-migration
Option '--skip-assignment' has been deprecated and will be removed in a future release.
The output includes credentials that you must protect. Be sure that you do not include these credentials in your code or check the credentials into your source control. For more information, see https://aka.ms/azadsp-cli
{
  "appId": "xxx",
  "displayName": "aks-tr",
  "password": "xxx",
  "tenant": "xxx"
}
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ az ad sp show --id xxx --query "objectId"
The underlying Active Directory Graph API will be replaced by Microsoft Graph API in Azure CLI 2.37.0. Please carefully review all breaking changes introduced during this migration: https://docs.microsoft.com/cli/azure/microsoft-graph-migration
"75686ebe-f809-4d6d-a1fc-3f5890a90975"
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ kubectl apply -f 01/rolebinding-dev-namespace.yaml 
rolebinding.rbac.authorization.k8s.io/dev-user-access configured
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ az login --service-principal -u xxx -p xxx --tenant xxx
No subscriptions found for xxx.
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ az account show
{
  "environmentName": "AzureCloud",
  "homeTenantId": "xxx",
  "id": "5f76c74a-70e8-4ee9-b1f7-1cdcbf7dbca9",
  "isDefault": true,
  "managedByTenants": [],
  "name": "Training",
  "state": "Enabled",
  "tenantId": "xxx",
  "user": {
    "name": "training00@xxx.io",
    "type": "user"
  }
}
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ az login --service-principal -u xxx -p xxx --tenant xxx
[
  {
    "cloudName": "AzureCloud",
    "homeTenantId": "xxx",
    "id": "5f76c74a-70e8-4ee9-b1f7-1cdcbf7dbca9",
    "isDefault": true,
    "managedByTenants": [],
    "name": "Training",
    "state": "Enabled",
    "tenantId": "xxx",
    "user": {
      "name": "xxx",
      "type": "servicePrincipal"
    }
  }
]
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ az aks get-credentials --resource-group azuread --name azuread
A different object named clusterUser_azuread_azuread already exists in your kubeconfig file.
Overwrite? (y/n): y
Merged "azuread" as current context in /home/vscode/.kube/config
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ az account show
{
  "environmentName": "AzureCloud",
  "homeTenantId": "xxx",
  "id": "5f76c74a-70e8-4ee9-b1f7-1cdcbf7dbca9",
  "isDefault": true,
  "managedByTenants": [],
  "name": "Training",
  "state": "Enabled",
  "tenantId": "xxx",
  "user": {
    "name": "xxx",
    "type": "servicePrincipal"
  }
}
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ az aks install-cli
Downloading client to "/usr/local/bin/kubectl" from "https://storage.googleapis.com/kubernetes-release/release/v1.23.6/bin/linux/amd64/kubectl"
Connection error while attempting to download client ([Errno 13] Permission denied: '/usr/local/bin/kubectl')
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ sudo az aks install-cli
Downloading client to "/usr/local/bin/kubectl" from "https://storage.googleapis.com/kubernetes-release/release/v1.23.6/bin/linux/amd64/kubectl"
Please ensure that /usr/local/bin is in your search PATH, so the `kubectl` command can be found.
Downloading client to "/tmp/tmp6yx_m56s/kubelogin.zip" from "https://github.com/Azure/kubelogin/releases/download/v0.0.13/kubelogin.zip"
Please ensure that /usr/local/bin is in your search PATH, so the `kubelogin` command can be found.
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ kubelogin convert-kubeconfig -l spn
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ AAD_SERVICE_PRINCIPAL_CLIENT_ID=xxx
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ AAD_SERVICE_PRINCIPAL_CLIENT_SECRET="xxx"
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ kubectl get no
Error: Both clientSecret and clientcert cannot be empty
Unable to connect to the server: getting credentials: exec: executable kubelogin failed with exit code 1
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ kubelogin
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ kubelogin convert-kubeconfig -l spn
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ kubectl get nodes
Error: Both clientSecret and clientcert cannot be empty
Unable to connect to the server: getting credentials: exec: executable kubelogin failed with exit code 1
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ cat ~/.kube/config 
apiVersion: v1
clusters:
- cluster:
    certificate-authority-data: LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSUU2VENDQXRHZ0F3SUJBZ0lSQUtoZ3V4VEtaelpjTEcxQkxYR2ZkR0V3RFFZSktvWklodmNOQVFFTEJRQXcKRFRFTE1Ba0dBMVVFQXhNQ1kyRXdJQmNOTWpJd05ESTRNRGd5TURRNFdoZ1BNakExTWpBME1qZ3dPRE13TkRoYQpNQTB4Q3pBSkJnTlZCQU1UQW1OaE1JSUNJakFOQmdrcWhraUc5dzBCQVFFRkFBT0NBZzhBTUlJQ0NnS0NBZ0VBCmwzT2ViQmhWazJZd0RiQVl2MmxyZm53ZW9Xcnc2R1dRTmtQSmZIdjdDamlaeTFWNitNemRKS1Y4U2Rzc09KVmEKUDl3dEJyZ1FTcml6L2dEV1RpcDdvWEgxTWxMTjdGK20xbVhOZ2RPblpKNmNxejBDVkx4Q2o2cVZEbDhmVmM0UwpoZWx3Nldub3FWRXFyTWh1bHB6T3dGTlAwNURBSVJjajBoQlNZR28yWTYzc0Vkek9VSXZxMGI4Z3p3dUF6bHVCCmw0M3kxN0doL2t5M2dCSDZzQTRwY3ZtSFZrd3FCZWxBa1BQWXk0ODJBL25DQ0o2Mzh0blJjSUNuRndva3BLaDUKcVBmRDNUV1dSZjBsY3hSdktpd0RxMExyQzNvQTY3UHFibE90bWVyQk9rRFh4anVZNjRXVkpIbXpaMVJSSEhRdApNVFJiUUZuQkR5eVIxWkJ4akZ4bjU5ZGFzQkxweFVYVXRTamQzVlVLWWdkelg2MjBFNjJ5bS9sUkFmVzFtQ2RoCmRzWVI0amNWUmRyVXlkQjk4WHN3OHgvcEdtcGpVSlU1WHRQOHVacWlCV2hSYXBraFBHUjYybTEvYkxoMlc3ZXYKZVRjZ3Rpd1lTSGlTSTJEUUxHbnFyZVU4Q3NtbDNyZ1UxamZ1ZVhFUFBla2ZUa0FId251bTZFbFlWdFhZT2h3cApjdjU5RjNBajZDNjh0dDVldENxcy9EcUhlaGR2OVR4ZmRscEErN1Y5UmRSSGhUVy9LSHBxdEliZ3FFSU5ZMmhKCkFLL2grTm1EZStqU3gzcStRUVhXajVHSjA4V1l3dnUydjllb0ZiL2VjMTZiWkQvTGFXdEVoV3Jwenl1dEQ2T0QKWU5nR3RLRlpOOXNKck9TcHdqdHY3WGs0MkJTK2tXbDlIaTVaMlZ2T1plc0NBd0VBQWFOQ01FQXdEZ1lEVlIwUApBUUgvQkFRREFnS2tNQThHQTFVZEV3RUIvd1FGTUFNQkFmOHdIUVlEVlIwT0JCWUVGRGxDN3ByaTRiYUJwQlg0Ck0zS1VUTmNtUDVkTE1BMEdDU3FHU0liM0RRRUJDd1VBQTRJQ0FRQ0dOdDFGV1Btc3lNaDh5RUJHM1pVZFIvaHIKeHBHRXp5M2dEYkhjRXRUeTNCbFBaOVY2Ukc2SXFHOFhzVlhkMzkvcURhL3ZMR3ZZak9ZeTltdlBBSTZOd3Q0NwpSdlZUZkRHK2RPVStlQzA5UUVwdlk5N05iL09zN1lDUFgyUGs4dEtQSTBsbjJmWGc4QnNRZ2QydG83NXVHWHBsCjloLzhnRG1PWFJ1MHFzOTh2UEMzLzRGMFprRkd3Z1YzRzdUbGJtUjUzWDdWdE9JdEU4SzVRWXBCekRUR3gzcnkKVUMwR3p1V0VWbzJyRXFsckRLc2VZbEY4Q2U5b3hCaGo4WmtPcExqQTBpdFZEOEJ1ZDNBcVBqc1Z2ejJFNU94cQp0VnQ3cDd0S3IvUWRHMVAvbnI4UkhQV0Y1dHBXS3hYQ1pCd2dVQTZwMHRNQW16YWFhNU9WamhFT0ZudFFTWFFGCnZGb1hvMVNyU1FEZ0IrbS9zYU92TWFhRFZOd0lLc3p0R2p5a2RSMU55bjZ1RlZVN3Nsd0szSnJJRVdQMTdEZEkKSjVReUVPUWEybmlweC9McVl3czFQNDIxZzZ1eVcweDNBNGRCYWI5R1BsS0U4V2R0cW9zYVA1YXRXaDVSeG42aApYOWltQU8rc2VFcnZ5bWU3aEN1Q1lVRnQ0NW5wLzlvU1hnV0ZXWWtzWk1BUlZ3dTdBTzNXOWRqQzFLYzR4ZjhXCjYrRlpramxFOERxVHJzR3pBMGxvcDJwY09hWFlSdXNTTDR2bmd2MWd4ckZDMmIvelIvd052ZVJScUpzSEtlaTMKZyt4R29QT21STkEwVUZjZTc5bVdFUFJvN2g1S0hWNVkxQVY3Nk83QWM0YWsvUVVtZ3hITnNucVNXN2k1RTZJUgpWVmpWRDBPRFBJOTgwcWdtQWc9PQotLS0tLUVORCBDRVJUSUZJQ0FURS0tLS0tCg==
    server: https://azuread-azuread-5f76c7-d0c6da74.hcp.eastus2.azmk8s.io:443
  name: azuread
contexts:
- context:
    cluster: azuread
    user: clusterUser_azuread_azuread
  name: azuread
current-context: azuread
kind: Config
preferences: {}
users:
- name: clusterUser_azuread_azuread
  user:
    exec:
      apiVersion: client.authentication.k8s.io/v1beta1
      args:
      - get-token
      - --environment
      - AzurePublicCloud
      - --server-id
      - xxx
      - --client-id
      - xxx
      - --tenant-id
      - xxx
      - --login
      - spn
      command: kubelogin
      env: null
      provideClusterInfo: false
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ history 
    1  az login --use-device-code 
    2  az aks create     --name azuread
    3  clear
    4  az aks create     --name azuread     --resource-group azuread     --disable-local-accounts     --enable-aad     --aad-admin-group-object-ids 8f1d7d0a-9b57-4e43-a543-144a8cdfa8bd
    5  clear
    6  az aks create     --name azuread     --resource-group azuread     --disable-local-accounts     --enable-aad     --no-ssh-key     --aad-admin-group-object-ids 8f1d7d0a-9b57-4e43-a543-144a8cdfa8bd
    7  clear
    8  az aks get-credentials --resource-group azuread --name azuread --help
    9  clear
   10  az aks get-credentials --resource-group azuread --name azuread --admin
   11  az aks get-credentials --resource-group azuread --name azuread 
   12  cat /home/vscode/.kube/config
   13  clear
   14  kubectl get nodes
   15  cat /home/vscode/.kube/config
   16  rm /home/vscode/.kube/config
   17  clear
   18  az aks get-credentials --resource-group azuread --name azuread 
   19  kubectl get nodes
   20  kubectl create namespace dev
   21  kubectl apply -f 01/role-dev-namespace.yaml 
   22  kubectl get sa -n dev
   23  kubectl get pod -n dev
   24  kubectl apply -f 01/rolebinding-dev-namespace.yaml 
   25  az ad sp create-for-rbac --skip-assignment --name aks-tr
   26  az ad sp show --id xxx --query "objectId"
   27  kubectl apply -f 01/rolebinding-dev-namespace.yaml 
   28  az login --service-principal -u xxx -p xxx --tenant xxx
   29  az account show
   30  az login --service-principal -u xxx -p xxx --tenant xxx
   31  az aks get-credentials --resource-group azuread --name azuread
   32  az account show
   33  az aks install-cli
   34  sudo az aks install-cli
   35  kubelogin convert-kubeconfig -l spn
   36  AAD_SERVICE_PRINCIPAL_CLIENT_ID=xxx
   37  AAD_SERVICE_PRINCIPAL_CLIENT_SECRET="xxx"
   38  kubectl get no
   39  kubelogin
   40  kubelogin convert-kubeconfig -l spn
   41  kubectl get nodes
   42  cat ~/.kube/config 
   43  history 
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ export AAD_SERVICE_PRINCIPAL_CLIENT_ID=xxx
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ export AAD_SERVICE_PRINCIPAL_CLIENT_SECRET="xxx"
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ kubectl get nodes
Error from server (Forbidden): nodes is forbidden: User "75686ebe-f809-4d6d-a1fc-3f5890a90975" cannot list resource "nodes" in API group "" at the cluster scope
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ kubectl get pod -n dev
No resources found in dev namespace.
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ kubectl create deployment nginx --image=nginx
error: failed to create deployment: deployments.apps is forbidden: User "75686ebe-f809-4d6d-a1fc-3f5890a90975" cannot create resource "deployments" in API group "apps" in the namespace "default"
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ kubectl create deployment nginx --image=nginx -n dev
deployment.apps/nginx created
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ history 
    1  az login --use-device-code 
    2  az aks create     --name azuread
    3  clear
    4  az aks create     --name azuread     --resource-group azuread     --disable-local-accounts     --enable-aad     --aad-admin-group-object-ids 8f1d7d0a-9b57-4e43-a543-144a8cdfa8bd
    5  clear
    6  az aks create     --name azuread     --resource-group azuread     --disable-local-accounts     --enable-aad     --no-ssh-key     --aad-admin-group-object-ids 8f1d7d0a-9b57-4e43-a543-144a8cdfa8bd
    7  clear
    8  az aks get-credentials --resource-group azuread --name azuread --help
    9  clear
   10  az aks get-credentials --resource-group azuread --name azuread --admin
   11  az aks get-credentials --resource-group azuread --name azuread 
   12  cat /home/vscode/.kube/config
   13  clear
   14  kubectl get nodes
   15  cat /home/vscode/.kube/config
   16  rm /home/vscode/.kube/config
   17  clear
   18  az aks get-credentials --resource-group azuread --name azuread 
   19  kubectl get nodes
   20  kubectl create namespace dev
   21  kubectl apply -f 01/role-dev-namespace.yaml 
   22  kubectl get sa -n dev
   23  kubectl get pod -n dev
   24  kubectl apply -f 01/rolebinding-dev-namespace.yaml 
   25  az ad sp create-for-rbac --skip-assignment --name aks-tr
   26  az ad sp show --id xxx --query "objectId"
   27  kubectl apply -f 01/rolebinding-dev-namespace.yaml 
   28  az login --service-principal -u xxx -p xxx --tenant xxx
   29  az account show
   30  az login --service-principal -u xxx -p xxx --tenant xxx
   31  az aks get-credentials --resource-group azuread --name azuread
   32  az account show
   33  az aks install-cli
   34  sudo az aks install-cli
   35  kubelogin convert-kubeconfig -l spn
   36  AAD_SERVICE_PRINCIPAL_CLIENT_ID=xxx
   37  AAD_SERVICE_PRINCIPAL_CLIENT_SECRET="xxx"
   38  kubectl get no
   39  kubelogin
   40  kubelogin convert-kubeconfig -l spn
   41  kubectl get nodes
   42  cat ~/.kube/config 
   43  history 
   44  export AAD_SERVICE_PRINCIPAL_CLIENT_ID=xxx
   45  export AAD_SERVICE_PRINCIPAL_CLIENT_SECRET="xxx"
   46  kubectl get nodes
   47  kubectl get pod -n dev
   48  kubectl create deployment nginx --image=nginx
   49  kubectl create deployment nginx --image=nginx -n dev
   50  history 
vscode ➜ /workspaces/azure-aks-ops (main) $ 