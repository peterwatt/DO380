# Authentication and Identity Management

## Goals

* Configure and manage OpenShift Authentication and Identities
* Integrate OpenShift with LDAP
* Integrate OpenShift with the Red Hat SSO OIDC (Keycloak)
* Manage multiple identity providers
* Configure authentication
* Configure and synchronize OpenShift groups
* Resolve synchronization conflicts
* Maintain group synchronization on a scheduled basis
* Configure RBAC roles with users and groups
* Create and use authentication tokens with kubeconfig files
* Create and use authentication certificates with kubeconfig files


## LDAP Group Synchronization

* LDAPSyncConfig

```bash
oc create sa rhds-group-syncer
oc create clusterrole rhds-group-syncer --verb get,list,create,update --resource groups
oc adm policy add-cluster-role-to-user rhds-group-syncer -z rhds-group-syncer
oc create secret generic rhds-secret --from-literal bindPassword='redhatocp'
```

* ConfigMap
* CronJob
