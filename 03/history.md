vscode ➜ /workspaces/azure-aks-ops (main ✗) $ rm ~/.kube/config 
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ az account list -o table
Name      CloudName    SubscriptionId                        State    IsDefault
--------  -----------  ------------------------------------  -------  -----------
Training  AzureCloud   5f76c74a-70e8-4ee9-b1f7-1cdcbf7dbca9  Enabled  True
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ az loing 
'loing' is misspelled or not recognized by the system.
Did you mean 'login' ?

Examples from AI knowledge base:
az login
Log in interactively.

az login -u johndoe@contoso.com -p VerySecret
Log in with user name and password. This doesn't work with Microsoft accounts or accounts that have two-factor authentication enabled. Use -p=secret if the first character of the password is '-'.

az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com
Log in with a service principal using client secret. Use -p=secret if the first character of the password is '-'.

https://aka.ms/cli_ref
Read more about the command in reference docs
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ az login
A web browser has been opened at https://login.microsoftonline.com/organizations/oauth2/v2.0/authorize. Please continue the login in the web browser. If no web browser is available or if the web browser fails to open, use device code flow with `az login --use-device-code`.
[
  {
    "cloudName": "AzureCloud",
    "homeTenantId": "xxx",
    "id": "xxx",
    "isDefault": true,
    "managedByTenants": [],
    "name": "Training",
    "state": "Enabled",
    "tenantId": "xxx",
    "user": {
      "name": "training00@xxx",
      "type": "user"
    }
  }
]
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ az aks get-credentials --resource-group azuread --name azuread
Merged "azuread" as current context in /home/vscode/.kube/config
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ kubectl get nodes
To sign in, use a web browser to open the page https://microsoft.com/devicelogin and enter the code DSJHSR228 to authenticate.
NAME                                STATUS   ROLES   AGE    VERSION
aks-nodepool1-34419311-vmss000000   Ready    agent   103m   v1.22.6
aks-nodepool1-34419311-vmss000001   Ready    agent   102m   v1.22.6
aks-nodepool1-34419311-vmss000002   Ready    agent   102m   v1.22.6
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ kubectl get pods -n kube-system 
NAME                                 READY   STATUS    RESTARTS   AGE
azure-ip-masq-agent-24s24            1/1     Running   0          103m
azure-ip-masq-agent-57fwg            1/1     Running   0          103m
azure-ip-masq-agent-gsb72            1/1     Running   0          103m
cloud-node-manager-cw4d7             1/1     Running   0          103m
cloud-node-manager-l2fnv             1/1     Running   0          103m
cloud-node-manager-m4k6n             1/1     Running   0          103m
coredns-69c47794-42dlc               1/1     Running   0          102m
coredns-69c47794-gnf6c               1/1     Running   0          104m
coredns-autoscaler-7d56cd888-p48hj   1/1     Running   0          104m
csi-azuredisk-node-2knjt             3/3     Running   0          103m
csi-azuredisk-node-5cbhn             3/3     Running   0          103m
csi-azuredisk-node-h8wst             3/3     Running   0          103m
csi-azurefile-node-227gl             3/3     Running   0          103m
csi-azurefile-node-9bd82             3/3     Running   0          103m
csi-azurefile-node-qc47r             3/3     Running   0          103m
kube-proxy-7bwbr                     1/1     Running   0          103m
kube-proxy-nb98f                     1/1     Running   0          103m
kube-proxy-tpjhq                     1/1     Running   0          103m
metrics-server-6576d9ccf8-6xqxb      1/1     Running   0          104m
tunnelfront-5d998c6cdf-tpc8z         1/1     Running   0          101m
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ kubectl apply -f 02/nginx.yaml 
deployment.apps/nginx created
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ kubectl describe pod nginx-5cfbc579c-75kmv
Name:           nginx-5cfbc579c-75kmv
Namespace:      default
Priority:       0
Node:           <none>
Labels:         app=nginx
                pod-template-hash=5cfbc579c
Annotations:    <none>
Status:         Pending
IP:             
IPs:            <none>
Controlled By:  ReplicaSet/nginx-5cfbc579c
Containers:
  nginx:
    Image:      nginx
    Port:       80/TCP
    Host Port:  0/TCP
    Limits:
      cpu:     500m
      memory:  128Mi
    Requests:
      cpu:        500m
      memory:     128Mi
    Environment:  <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-tbrhw (ro)
Conditions:
  Type           Status
  PodScheduled   False 
Volumes:
  kube-api-access-tbrhw:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   Guaranteed
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/memory-pressure:NoSchedule op=Exists
                             node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type     Reason            Age   From                Message
  ----     ------            ----  ----                -------
  Warning  FailedScheduling  16s   default-scheduler   0/3 nodes are available: 3 Insufficient cpu.
  Normal   TriggeredScaleUp  7s    cluster-autoscaler  pod triggered scale-up: [{aks-nodepool1-34419311-vmss 3->5 (max: 5)}]
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ kubectl get nodes
NAME                                STATUS   ROLES    AGE    VERSION
aks-nodepool1-34419311-vmss000000   Ready    agent    111m   v1.22.6
aks-nodepool1-34419311-vmss000001   Ready    agent    111m   v1.22.6
aks-nodepool1-34419311-vmss000002   Ready    agent    111m   v1.22.6
aks-nodepool1-34419311-vmss000004   Ready    <none>   6s     v1.22.6
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ kubectl apply -f 02/nginx.yaml 
deployment.apps/nginx configured
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ kubectl apply -f 02/nginx.yaml 
deployment.apps/nginx configured
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ kubectl apply -f https://github.com/kedacore/keda/releases/download/v2.6.1/keda-2.6.1.yaml
namespace/keda created
customresourcedefinition.apiextensions.k8s.io/clustertriggerauthentications.keda.sh created
customresourcedefinition.apiextensions.k8s.io/scaledjobs.keda.sh created
customresourcedefinition.apiextensions.k8s.io/scaledobjects.keda.sh created
customresourcedefinition.apiextensions.k8s.io/triggerauthentications.keda.sh created
serviceaccount/keda-operator created
clusterrole.rbac.authorization.k8s.io/keda-external-metrics-reader created
clusterrole.rbac.authorization.k8s.io/keda-operator created
rolebinding.rbac.authorization.k8s.io/keda-auth-reader created
clusterrolebinding.rbac.authorization.k8s.io/keda-hpa-controller-external-metrics created
clusterrolebinding.rbac.authorization.k8s.io/keda-operator created
clusterrolebinding.rbac.authorization.k8s.io/keda-system-auth-delegator created
service/keda-metrics-apiserver created
deployment.apps/keda-metrics-apiserver created
deployment.apps/keda-operator created
apiservice.apiregistration.k8s.io/v1beta1.external.metrics.k8s.io created
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ kubectl apply -f 02/deployment.yaml 
deployment.apps/contoso-microservice created
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ kubectl apply -f 02/keda.yaml 
scaledobject.keda.sh/scaled-contoso created
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ kubectl get pods
NAME                    READY   STATUS    RESTARTS   AGE
nginx-5cfbc579c-srh98   1/1     Running   0          71m
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ kubectl get pods
NAME                    READY   STATUS    RESTARTS   AGE
nginx-5cfbc579c-srh98   1/1     Running   0          71m
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ kubectl get pods
NAME                    READY   STATUS    RESTARTS   AGE
nginx-5cfbc579c-srh98   1/1     Running   0          71m
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ kubectl get pods
NAME                    READY   STATUS    RESTARTS   AGE
nginx-5cfbc579c-srh98   1/1     Running   0          71m
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ kubectl get pods
NAME                    READY   STATUS    RESTARTS   AGE
nginx-5cfbc579c-srh98   1/1     Running   0          71m
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ kubectl get pods -A
NAMESPACE     NAME                                      READY   STATUS    RESTARTS   AGE
default       nginx-5cfbc579c-srh98                     1/1     Running   0          73m
dev           nginx-6799fc88d8-v97gs                    1/1     Running   0          73m
keda          keda-metrics-apiserver-59b9ddc78c-5mwb6   1/1     Running   0          65m
keda          keda-operator-f76d844d7-gt5tw             1/1     Running   0          65m
kube-system   azure-ip-masq-agent-42v4z                 1/1     Running   0          5m20s
kube-system   azure-ip-masq-agent-57fwg                 1/1     Running   0          3h17m
kube-system   azure-ip-masq-agent-zlvbc                 1/1     Running   0          5m34s
kube-system   cloud-node-manager-bvjh5                  1/1     Running   0          5m34s
kube-system   cloud-node-manager-drflk                  1/1     Running   0          5m20s
kube-system   cloud-node-manager-m4k6n                  1/1     Running   0          3h17m
kube-system   coredns-69c47794-42dlc                    1/1     Running   0          3h16m
kube-system   coredns-69c47794-gnf6c                    1/1     Running   0          3h18m
kube-system   coredns-autoscaler-7d56cd888-p48hj        1/1     Running   0          3h18m
kube-system   csi-azuredisk-node-56v6w                  3/3     Running   0          5m20s
kube-system   csi-azuredisk-node-5cbhn                  3/3     Running   0          3h17m
kube-system   csi-azuredisk-node-flbc6                  3/3     Running   0          5m34s
kube-system   csi-azurefile-node-5bn2d                  3/3     Running   0          5m20s
kube-system   csi-azurefile-node-9bd82                  3/3     Running   0          3h17m
kube-system   csi-azurefile-node-g8cwh                  3/3     Running   0          5m34s
kube-system   kube-proxy-7qp9n                          1/1     Running   0          5m20s
kube-system   kube-proxy-nb98f                          1/1     Running   0          3h17m
kube-system   kube-proxy-rjbbz                          1/1     Running   0          5m34s
kube-system   metrics-server-6576d9ccf8-6xqxb           1/1     Running   0          3h18m
kube-system   tunnelfront-5d998c6cdf-tpc8z              1/1     Running   0          3h16m
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ kubectl delete ns dev
namespace "dev" deleted
^C
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ kubectl delete deployments.apps nginx 
deployment.apps "nginx" deleted
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ az aks update \
    --name azuread \
    --resource-group azuread \
    --cluster-autoscaler-profile expander=priority
{
  "aadProfile": {
    "adminGroupObjectIDs": [
      "8f1d7d0a-9b57-4e43-a543-144a8cdfa8bd"
    ],
    "adminUsers": null,
    "clientAppId": null,
    "enableAzureRbac": false,
    "managed": true,
    "serverAppId": null,
    "serverAppSecret": null,
    "tenantId": "xxx"
  },
  "addonProfiles": null,
  "agentPoolProfiles": [
    {
      "availabilityZones": null,
      "count": 1,
      "creationData": null,
      "enableAutoScaling": true,
      "enableEncryptionAtHost": false,
      "enableFips": false,
      "enableNodePublicIp": false,
      "enableUltraSsd": false,
      "gpuInstanceProfile": null,
      "kubeletConfig": null,
      "kubeletDiskType": "OS",
      "linuxOsConfig": null,
      "maxCount": 2,
      "maxPods": 110,
      "minCount": 1,
      "mode": "System",
      "name": "nodepool1",
      "nodeImageVersion": "AKSUbuntu-1804gen2containerd-2022.04.05",
      "nodeLabels": null,
      "nodePublicIpPrefixId": null,
      "nodeTaints": null,
      "orchestratorVersion": "1.22.6",
      "osDiskSizeGb": 128,
      "osDiskType": "Managed",
      "osSku": "Ubuntu",
      "osType": "Linux",
      "podSubnetId": null,
      "powerState": {
        "code": "Running"
      },
      "provisioningState": "Succeeded",
      "proximityPlacementGroupId": null,
      "scaleDownMode": null,
      "scaleSetEvictionPolicy": null,
      "scaleSetPriority": null,
      "spotMaxPrice": null,
      "tags": null,
      "type": "VirtualMachineScaleSets",
      "upgradeSettings": null,
      "vmSize": "Standard_DS2_v2",
      "vnetSubnetId": null,
      "workloadRuntime": null
    },
    {
      "availabilityZones": null,
      "count": 0,
      "creationData": null,
      "enableAutoScaling": true,
      "enableEncryptionAtHost": null,
      "enableFips": false,
      "enableNodePublicIp": false,
      "enableUltraSsd": null,
      "gpuInstanceProfile": null,
      "kubeletConfig": null,
      "kubeletDiskType": "OS",
      "linuxOsConfig": null,
      "maxCount": 2,
      "maxPods": 110,
      "minCount": 0,
      "mode": "User",
      "name": "spot",
      "nodeImageVersion": "AKSUbuntu-1804gen2containerd-2022.04.13",
      "nodeLabels": null,
      "nodePublicIpPrefixId": null,
      "nodeTaints": null,
      "orchestratorVersion": "1.22.6",
      "osDiskSizeGb": 128,
      "osDiskType": "Managed",
      "osSku": "Ubuntu",
      "osType": "Linux",
      "podSubnetId": null,
      "powerState": {
        "code": "Running"
      },
      "provisioningState": "Succeeded",
      "proximityPlacementGroupId": null,
      "scaleDownMode": "Delete",
      "scaleSetEvictionPolicy": null,
      "scaleSetPriority": null,
      "spotMaxPrice": null,
      "tags": null,
      "type": "VirtualMachineScaleSets",
      "upgradeSettings": {
        "maxSurge": null
      },
      "vmSize": "Standard_D2s_v3",
      "vnetSubnetId": null,
      "workloadRuntime": null
    }
  ],
  "apiServerAccessProfile": null,
  "autoScalerProfile": {
    "balanceSimilarNodeGroups": "false",
    "expander": "priority",
    "maxEmptyBulkDelete": "10",
    "maxGracefulTerminationSec": "600",
    "maxNodeProvisionTime": "15m",
    "maxTotalUnreadyPercentage": "45",
    "newPodScaleUpDelay": "0s",
    "okTotalUnreadyCount": "3",
    "scaleDownDelayAfterAdd": "10m",
    "scaleDownDelayAfterDelete": "10s",
    "scaleDownDelayAfterFailure": "3m",
    "scaleDownUnneededTime": "10m",
    "scaleDownUnreadyTime": "20m",
    "scaleDownUtilizationThreshold": "0.5",
    "scanInterval": "10s",
    "skipNodesWithLocalStorage": "false",
    "skipNodesWithSystemPods": "true"
  },
  "autoUpgradeProfile": null,
  "azurePortalFqdn": "azuread-azuread-5f76c7-d0c6da74.portal.hcp.eastus2.azmk8s.io",
  "disableLocalAccounts": true,
  "diskEncryptionSetId": null,
  "dnsPrefix": "azuread-azuread-5f76c7",
  "enablePodSecurityPolicy": null,
  "enableRbac": true,
  "extendedLocation": null,
  "fqdn": "azuread-azuread-5f76c7-d0c6da74.hcp.eastus2.azmk8s.io",
  "fqdnSubdomain": null,
  "httpProxyConfig": null,
  "id": "/subscriptions/5f76c74a-70e8-4ee9-b1f7-1cdcbf7dbca9/resourcegroups/azuread/providers/Microsoft.ContainerService/managedClusters/azuread",
  "identity": {
    "principalId": "933931bd-2cf4-48d6-803c-33d507e43b36",
    "tenantId": "xxx",
    "type": "SystemAssigned",
    "userAssignedIdentities": null
  },
  "identityProfile": {
    "kubeletidentity": {
      "clientId": "dd7143eb-1c7c-490a-9fc3-895f783841b2",
      "objectId": "842e49c1-d2dc-46f8-a3f2-772b00eb737f",
      "resourceId": "/subscriptions/5f76c74a-70e8-4ee9-b1f7-1cdcbf7dbca9/resourcegroups/MC_azuread_azuread_eastus2/providers/Microsoft.ManagedIdentity/userAssignedIdentities/azuread-agentpool"
    }
  },
  "kubernetesVersion": "1.22.6",
  "linuxProfile": null,
  "location": "eastus2",
  "maxAgentPools": 100,
  "name": "azuread",
  "networkProfile": {
    "dnsServiceIp": "10.0.0.10",
    "dockerBridgeCidr": "172.17.0.1/16",
    "ipFamilies": [
      "IPv4"
    ],
    "loadBalancerProfile": {
      "allocatedOutboundPorts": null,
      "effectiveOutboundIPs": [
        {
          "id": "/subscriptions/5f76c74a-70e8-4ee9-b1f7-1cdcbf7dbca9/resourceGroups/MC_azuread_azuread_eastus2/providers/Microsoft.Network/publicIPAddresses/5a71be26-ae2f-475b-91e5-f7362eaccf40",
          "resourceGroup": "MC_azuread_azuread_eastus2"
        }
      ],
      "enableMultipleStandardLoadBalancers": null,
      "idleTimeoutInMinutes": null,
      "managedOutboundIPs": {
        "count": 1,
        "countIpv6": null
      },
      "outboundIPs": null,
      "outboundIpPrefixes": null
    },
    "loadBalancerSku": "Standard",
    "natGatewayProfile": null,
    "networkMode": null,
    "networkPlugin": "kubenet",
    "networkPolicy": null,
    "outboundType": "loadBalancer",
    "podCidr": "10.244.0.0/16",
    "podCidrs": [
      "10.244.0.0/16"
    ],
    "serviceCidr": "10.0.0.0/16",
    "serviceCidrs": [
      "10.0.0.0/16"
    ]
  },
  "nodeResourceGroup": "MC_azuread_azuread_eastus2",
  "podIdentityProfile": null,
  "powerState": {
    "code": "Running"
  },
  "privateFqdn": null,
  "privateLinkResources": null,
  "provisioningState": "Succeeded",
  "publicNetworkAccess": null,
  "resourceGroup": "azuread",
  "securityProfile": {
    "azureDefender": null
  },
  "servicePrincipalProfile": {
    "clientId": "msi",
    "secret": null
  },
  "sku": {
    "name": "Basic",
    "tier": "Free"
  },
  "systemData": null,
  "tags": null,
  "type": "Microsoft.ContainerService/ManagedClusters",
  "windowsProfile": null
}
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ kubectl get nodes
NAME                                STATUS   ROLES   AGE     VERSION
aks-nodepool1-34419311-vmss000000   Ready    agent   3h28m   v1.22.6
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ kubectl apply -f 02/cluster-autoscaler-priority-expander.yaml 
configmap/cluster-autoscaler-priority-expander created
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ kubectl get cm -n kube-system
NAME                                   DATA   AGE
azure-ip-masq-agent-config             1      3h30m
cluster-autoscaler-priority-expander   1      46s
cluster-autoscaler-status              1      5m55s
coredns                                1      3h30m
coredns-autoscaler                     1      3h28m
coredns-custom                         0      3h30m
extension-apiserver-authentication     6      3h30m
kube-root-ca.crt                       1      3h30m
overlay-upgrade-data                   4      3h30m
tunnelfront-kubecfg                    1      3h30m
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ kubectl get -o yaml -n kube-system cluster-autoscaler-status
error: the server doesn't have a resource type "cluster-autoscaler-status"
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ kubectl get -o yaml -n kube-system cm cluster-autoscaler-status
apiVersion: v1
data:
  status: |+
    Cluster-autoscaler status at 2022-04-28 12:02:52.497530546 +0000 UTC:
    Cluster-wide:
      Health:      Healthy (ready=1 unready=0 notStarted=0 longNotStarted=0 registered=1 longUnregistered=0)
                   LastProbeTime:      2022-04-28 12:02:52.4903102 +0000 UTC m=+6242.512006764
                   LastTransitionTime: 2022-04-28 11:56:41.238727561 +0000 UTC m=+5871.260424125
      ScaleUp:     NoActivity (ready=1 registered=1)
                   LastProbeTime:      2022-04-28 12:02:52.4903102 +0000 UTC m=+6242.512006764
                   LastTransitionTime: 2022-04-28 11:56:41.238727561 +0000 UTC m=+5871.260424125
      ScaleDown:   NoCandidates (candidates=0)
                   LastProbeTime:      2022-04-28 12:02:52.4903102 +0000 UTC m=+6242.512006764
                   LastTransitionTime: 2022-04-28 11:56:41.238727561 +0000 UTC m=+5871.260424125

    NodeGroups:
      Name:        aks-nodepool1-34419311-vmss
      Health:      Healthy (ready=1 unready=0 notStarted=0 longNotStarted=0 registered=1 longUnregistered=0 cloudProviderTarget=1 (minSize=1, maxSize=2))
                   LastProbeTime:      2022-04-28 12:02:52.4903102 +0000 UTC m=+6242.512006764
                   LastTransitionTime: 2022-04-28 11:56:41.238727561 +0000 UTC m=+5871.260424125
      ScaleUp:     NoActivity (ready=1 cloudProviderTarget=1)
                   LastProbeTime:      2022-04-28 12:02:52.4903102 +0000 UTC m=+6242.512006764
                   LastTransitionTime: 2022-04-28 11:56:41.238727561 +0000 UTC m=+5871.260424125
      ScaleDown:   NoCandidates (candidates=0)
                   LastProbeTime:      2022-04-28 12:02:52.4903102 +0000 UTC m=+6242.512006764
                   LastTransitionTime: 2022-04-28 11:56:41.238727561 +0000 UTC m=+5871.260424125

      Name:        aks-spot-74243589-vmss
      Health:      Healthy (ready=0 unready=0 notStarted=0 longNotStarted=0 registered=0 longUnregistered=0 cloudProviderTarget=0 (minSize=0, maxSize=2))
                   LastProbeTime:      0001-01-01 00:00:00 +0000 UTC
                   LastTransitionTime: 0001-01-01 00:00:00 +0000 UTC
      ScaleUp:     NoActivity (ready=0 cloudProviderTarget=0)
                   LastProbeTime:      0001-01-01 00:00:00 +0000 UTC
                   LastTransitionTime: 0001-01-01 00:00:00 +0000 UTC
      ScaleDown:   NoCandidates (candidates=0)
                   LastProbeTime:      2022-04-28 12:02:52.4903102 +0000 UTC m=+6242.512006764
                   LastTransitionTime: 2022-04-28 11:56:41.238727561 +0000 UTC m=+5871.260424125

kind: ConfigMap
metadata:
  annotations:
    cluster-autoscaler.kubernetes.io/last-updated: 2022-04-28 12:02:52.497530546 +0000
      UTC
  creationTimestamp: "2022-04-28T11:56:41Z"
  name: cluster-autoscaler-status
  namespace: kube-system
  resourceVersion: "54555"
  uid: 8852f0f6-e2b8-4882-9d0c-2177019ecf2a
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ kubectl get pods -w 
NAME                                   READY   STATUS    RESTARTS   AGE
contoso-microservice-796dd57b7-4tnwt   0/1     Pending   0          0s
contoso-microservice-796dd57b7-4tnwt   0/1     Pending   0          0s
contoso-microservice-796dd57b7-4tnwt   0/1     ContainerCreating   0          0s
contoso-microservice-796dd57b7-4tnwt   1/1     Running             0          2s
contoso-microservice-796dd57b7-gqj5q   0/1     Pending             0          0s
contoso-microservice-796dd57b7-49dkw   0/1     Pending             0          0s
contoso-microservice-796dd57b7-9fl8h   0/1     Pending             0          0s
contoso-microservice-796dd57b7-gqj5q   0/1     Pending             0          0s
contoso-microservice-796dd57b7-9pp5k   0/1     Pending             0          0s
contoso-microservice-796dd57b7-49dkw   0/1     Pending             0          0s
contoso-microservice-796dd57b7-9fl8h   0/1     Pending             0          0s
contoso-microservice-796dd57b7-9pp5k   0/1     Pending             0          0s
contoso-microservice-796dd57b7-4mts7   0/1     Pending             0          0s
contoso-microservice-796dd57b7-4mts7   0/1     Pending             0          0s
contoso-microservice-796dd57b7-n6ttb   0/1     Pending             0          0s
contoso-microservice-796dd57b7-6t2lq   0/1     Pending             0          0s
contoso-microservice-796dd57b7-n6ttb   0/1     Pending             0          0s
contoso-microservice-796dd57b7-ksp85   0/1     Pending             0          0s
contoso-microservice-796dd57b7-ttkz2   0/1     Pending             0          0s
contoso-microservice-796dd57b7-6t2lq   0/1     Pending             0          0s
contoso-microservice-796dd57b7-ksp85   0/1     Pending             0          0s
contoso-microservice-796dd57b7-ttkz2   0/1     Pending             0          0s
contoso-microservice-796dd57b7-p4lm9   0/1     Pending             0          0s
contoso-microservice-796dd57b7-gpcq6   0/1     Pending             0          0s
contoso-microservice-796dd57b7-9sbgl   0/1     Pending             0          0s
contoso-microservice-796dd57b7-p4lm9   0/1     Pending             0          0s
contoso-microservice-796dd57b7-kqs5s   0/1     Pending             0          0s
contoso-microservice-796dd57b7-qqwfv   0/1     Pending             0          0s
contoso-microservice-796dd57b7-gpcq6   0/1     Pending             0          0s
contoso-microservice-796dd57b7-xgztc   0/1     Pending             0          0s
contoso-microservice-796dd57b7-ns97r   0/1     Pending             0          0s
contoso-microservice-796dd57b7-9sbgl   0/1     Pending             0          0s
contoso-microservice-796dd57b7-fn6pv   0/1     Pending             0          0s
contoso-microservice-796dd57b7-5q5f4   0/1     Pending             0          0s
contoso-microservice-796dd57b7-k8b28   0/1     Pending             0          0s
contoso-microservice-796dd57b7-kqs5s   0/1     Pending             0          0s
contoso-microservice-796dd57b7-qqwfv   0/1     Pending             0          0s
contoso-microservice-796dd57b7-xgztc   0/1     Pending             0          0s
contoso-microservice-796dd57b7-ns97r   0/1     Pending             0          0s
contoso-microservice-796dd57b7-fn6pv   0/1     Pending             0          0s
contoso-microservice-796dd57b7-5q5f4   0/1     Pending             0          0s
contoso-microservice-796dd57b7-k8b28   0/1     Pending             0          0s
contoso-microservice-796dd57b7-gqj5q   0/1     Pending             0          2m10s
contoso-microservice-796dd57b7-49dkw   0/1     Pending             0          2m10s
contoso-microservice-796dd57b7-9fl8h   0/1     Pending             0          2m10s
contoso-microservice-796dd57b7-9pp5k   0/1     Pending             0          2m10s
contoso-microservice-796dd57b7-4mts7   0/1     Pending             0          2m25s
contoso-microservice-796dd57b7-n6ttb   0/1     Pending             0          2m25s
contoso-microservice-796dd57b7-6t2lq   0/1     Pending             0          2m25s
contoso-microservice-796dd57b7-ksp85   0/1     Pending             0          2m25s
contoso-microservice-796dd57b7-ttkz2   0/1     Pending             0          2m25s
contoso-microservice-796dd57b7-p4lm9   0/1     Pending             0          2m10s
contoso-microservice-796dd57b7-gpcq6   0/1     Pending             0          2m10s
contoso-microservice-796dd57b7-9sbgl   0/1     Pending             0          2m10s
contoso-microservice-796dd57b7-kqs5s   0/1     Pending             0          2m10s
contoso-microservice-796dd57b7-qqwfv   0/1     Pending             0          2m10s
contoso-microservice-796dd57b7-xgztc   0/1     Pending             0          2m10s
contoso-microservice-796dd57b7-ns97r   0/1     Pending             0          2m10s
contoso-microservice-796dd57b7-fn6pv   0/1     Pending             0          2m10s
contoso-microservice-796dd57b7-5q5f4   0/1     Pending             0          2m10s
contoso-microservice-796dd57b7-gqj5q   0/1     Pending             0          2m54s
contoso-microservice-796dd57b7-49dkw   0/1     Pending             0          2m54s
contoso-microservice-796dd57b7-9fl8h   0/1     Pending             0          2m54s
contoso-microservice-796dd57b7-9pp5k   0/1     Pending             0          2m54s
contoso-microservice-796dd57b7-gqj5q   0/1     ContainerCreating   0          2m54s
contoso-microservice-796dd57b7-4mts7   0/1     Pending             0          2m39s
contoso-microservice-796dd57b7-9fl8h   0/1     ContainerCreating   0          2m54s
contoso-microservice-796dd57b7-n6ttb   0/1     Pending             0          2m39s
contoso-microservice-796dd57b7-6t2lq   0/1     Pending             0          2m39s
contoso-microservice-796dd57b7-ksp85   0/1     Pending             0          2m39s
contoso-microservice-796dd57b7-ttkz2   0/1     Pending             0          2m39s
contoso-microservice-796dd57b7-p4lm9   0/1     Pending             0          2m24s
contoso-microservice-796dd57b7-gpcq6   0/1     Pending             0          2m24s
contoso-microservice-796dd57b7-9sbgl   0/1     Pending             0          2m24s
contoso-microservice-796dd57b7-kqs5s   0/1     Pending             0          2m24s
contoso-microservice-796dd57b7-qqwfv   0/1     Pending             0          2m24s
contoso-microservice-796dd57b7-xgztc   0/1     Pending             0          2m24s
contoso-microservice-796dd57b7-ns97r   0/1     Pending             0          2m24s
contoso-microservice-796dd57b7-fn6pv   0/1     Pending             0          2m24s
contoso-microservice-796dd57b7-5q5f4   0/1     Pending             0          2m24s
contoso-microservice-796dd57b7-9fl8h   1/1     Running             0          2m56s
contoso-microservice-796dd57b7-gqj5q   1/1     Running             0          2m57s
contoso-microservice-796dd57b7-49dkw   0/1     Pending             0          3m3s
contoso-microservice-796dd57b7-k8b28   0/1     Pending             0          2m40s
contoso-microservice-796dd57b7-9fl8h   0/1     Error               0          3m16s
contoso-microservice-796dd57b7-gqj5q   0/1     Error               0          3m17s
contoso-microservice-796dd57b7-9fl8h   1/1     Running             1 (1s ago)   3m17s
contoso-microservice-796dd57b7-gqj5q   1/1     Running             1 (2s ago)   3m18s
contoso-microservice-796dd57b7-9pp5k   0/1     Pending             0            3m54s
contoso-microservice-796dd57b7-4mts7   0/1     Pending             0            3m39s
contoso-microservice-796dd57b7-n6ttb   0/1     Pending             0            3m39s
contoso-microservice-796dd57b7-6t2lq   0/1     Pending             0            3m39s
contoso-microservice-796dd57b7-ksp85   0/1     Pending             0            3m39s
contoso-microservice-796dd57b7-9pp5k   0/1     ContainerCreating   0            3m54s
contoso-microservice-796dd57b7-ttkz2   0/1     Pending             0            3m39s
contoso-microservice-796dd57b7-p4lm9   0/1     Pending             0            3m24s
contoso-microservice-796dd57b7-gpcq6   0/1     Pending             0            3m24s
contoso-microservice-796dd57b7-9sbgl   0/1     Pending             0            3m24s
contoso-microservice-796dd57b7-kqs5s   0/1     Pending             0            3m24s
contoso-microservice-796dd57b7-qqwfv   0/1     Pending             0            3m24s
contoso-microservice-796dd57b7-xgztc   0/1     Pending             0            3m24s
contoso-microservice-796dd57b7-ns97r   0/1     Pending             0            3m24s
contoso-microservice-796dd57b7-fn6pv   0/1     Pending             0            3m24s
contoso-microservice-796dd57b7-5q5f4   0/1     Pending             0            3m24s
contoso-microservice-796dd57b7-49dkw   0/1     Pending             0            3m54s
contoso-microservice-796dd57b7-k8b28   0/1     Pending             0            3m24s
^Cvscode ➜ /workspaces/azure-aks-ops (main ✗) $ ^C
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ kubectl get pod
NAME                                   READY   STATUS    RESTARTS      AGE
contoso-microservice-796dd57b7-49dkw   0/1     Pending   0             4m12s
contoso-microservice-796dd57b7-4mts7   0/1     Pending   0             3m57s
contoso-microservice-796dd57b7-4tnwt   1/1     Running   0             4m26s
contoso-microservice-796dd57b7-5q5f4   0/1     Pending   0             3m42s
contoso-microservice-796dd57b7-6t2lq   0/1     Pending   0             3m57s
contoso-microservice-796dd57b7-9fl8h   1/1     Running   1 (56s ago)   4m12s
contoso-microservice-796dd57b7-9pp5k   1/1     Running   0             4m12s
contoso-microservice-796dd57b7-9sbgl   0/1     Pending   0             3m42s
contoso-microservice-796dd57b7-fn6pv   0/1     Pending   0             3m42s
contoso-microservice-796dd57b7-gpcq6   0/1     Pending   0             3m42s
contoso-microservice-796dd57b7-gqj5q   1/1     Running   1 (56s ago)   4m12s
contoso-microservice-796dd57b7-k8b28   0/1     Pending   0             3m42s
contoso-microservice-796dd57b7-kqs5s   0/1     Pending   0             3m42s
contoso-microservice-796dd57b7-ksp85   0/1     Pending   0             3m57s
contoso-microservice-796dd57b7-n6ttb   0/1     Pending   0             3m57s
contoso-microservice-796dd57b7-ns97r   0/1     Pending   0             3m42s
contoso-microservice-796dd57b7-p4lm9   0/1     Pending   0             3m42s
contoso-microservice-796dd57b7-qqwfv   0/1     Pending   0             3m42s
contoso-microservice-796dd57b7-ttkz2   0/1     Pending   0             3m57s
contoso-microservice-796dd57b7-xgztc   0/1     Pending   0             3m42s
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ kubectl get nodes
NAME                                STATUS   ROLES   AGE     VERSION
aks-nodepool1-34419311-vmss000000   Ready    agent   3h38m   v1.22.6
aks-nodepool1-34419311-vmss000005   Ready    agent   2m15s   v1.22.6
aks-spot-74243589-vmss000002        Ready    agent   2m4s    v1.22.6
aks-spot-74243589-vmss000003        Ready    agent   2m12s   v1.22.6
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ kubectl get pod
NAME                                   READY   STATUS    RESTARTS        AGE
contoso-microservice-796dd57b7-49dkw   0/1     Pending   0               7m40s
contoso-microservice-796dd57b7-4mts7   0/1     Pending   0               7m25s
contoso-microservice-796dd57b7-4tnwt   1/1     Running   0               7m54s
contoso-microservice-796dd57b7-5q5f4   0/1     Pending   0               7m10s
contoso-microservice-796dd57b7-6t2lq   0/1     Pending   0               7m25s
contoso-microservice-796dd57b7-9fl8h   1/1     Running   1 (4m24s ago)   7m40s
contoso-microservice-796dd57b7-9pp5k   1/1     Running   1 (3m25s ago)   7m40s
contoso-microservice-796dd57b7-9sbgl   0/1     Pending   0               7m10s
contoso-microservice-796dd57b7-fn6pv   0/1     Pending   0               7m10s
contoso-microservice-796dd57b7-gpcq6   0/1     Pending   0               7m10s
contoso-microservice-796dd57b7-gqj5q   1/1     Running   1 (4m24s ago)   7m40s
contoso-microservice-796dd57b7-k8b28   0/1     Pending   0               7m10s
contoso-microservice-796dd57b7-kqs5s   0/1     Pending   0               7m10s
contoso-microservice-796dd57b7-ksp85   0/1     Pending   0               7m25s
contoso-microservice-796dd57b7-n6ttb   0/1     Pending   0               7m25s
contoso-microservice-796dd57b7-ns97r   0/1     Pending   0               7m10s
contoso-microservice-796dd57b7-p4lm9   0/1     Pending   0               7m10s
contoso-microservice-796dd57b7-qqwfv   0/1     Pending   0               7m10s
contoso-microservice-796dd57b7-ttkz2   0/1     Pending   0               7m25s
contoso-microservice-796dd57b7-xgztc   0/1     Pending   0               7m10s
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ kubectl get pod
No resources found in default namespace.
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ kubectl get nodes -w
NAME                                STATUS   ROLES   AGE     VERSION
aks-nodepool1-34419311-vmss000000   Ready    agent   4h25m   v1.22.6
^Cvscode ➜ /workspaces/azure-aks-ops (main ✗) $ # 04
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ az aks enable-addons -a monitoring -g azuread -n azuread
(OperationNotAllowed) Operation is not allowed: Another operation (nodepool1 - Upgrading) is in progress, please wait for it to finish before starting a new operation. See https://aka.ms/aks-pending-operation for more details
Code: OperationNotAllowed
Message: Operation is not allowed: Another operation (nodepool1 - Upgrading) is in progress, please wait for it to finish before starting a new operation. See https://aka.ms/aks-pending-operation for more details
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ kubectl get pods -n kube-system
NAME                                 READY   STATUS    RESTARTS   AGE
azure-ip-masq-agent-8qksv            1/1     Running   0          16m
azure-ip-masq-agent-j2f6k            1/1     Running   0          14m
cloud-node-manager-w8fk9             1/1     Running   0          16m
cloud-node-manager-wxdwf             1/1     Running   0          14m
coredns-69c47794-4bmzc               1/1     Running   0          13m
coredns-69c47794-l2njx               1/1     Running   0          13m
coredns-autoscaler-7d56cd888-ftzns   1/1     Running   0          13m
csi-azuredisk-node-f4t7p             3/3     Running   0          14m
csi-azuredisk-node-jjcvr             3/3     Running   0          16m
csi-azurefile-node-d6jd8             3/3     Running   0          14m
csi-azurefile-node-hhkp7             3/3     Running   0          16m
kube-proxy-4f9sz                     1/1     Running   0          16m
kube-proxy-8gm5n                     1/1     Running   0          14m
metrics-server-6576d9ccf8-8j4c6      1/1     Running   0          12m
metrics-server-6576d9ccf8-thbqh      1/1     Running   0          13m
tunnelfront-5d998c6cdf-nwv5j         1/1     Running   0          13m
vscode ➜ /workspaces/azure-aks-ops (main ✗) $ 