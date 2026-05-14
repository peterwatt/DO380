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

## Deleting kubeadmin

## Authenticating using LDAP

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

## OIDC Authentication and Group Claims

`OIDC` stands for `OpenID Connect`

1. Obtain the client ID and the client secret from the OIDC IdP client for the OpenShift integration.

2. Create an OpenShift `secret` object, which contains the client secret that is obtained from the OIDC client configuration, in the openshift-config namespace.

3. Create an OpenShift `configmap` object, which contains the certificate authority bundle in the ca.crt file parameter, in the openshift-config namespace (this step is required only if the CA certificate is not configured as a system-wide CA).

4. Create the `OAuth` CR YAML file to include the OIDC IdP. Apply the configuration file to the OAuth CR.

```bash
 oc get useroauthaccesstokens
```
