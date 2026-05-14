# Authentication and Identity Management

## Goals

* Configure and manage OpenShift Authentication and Identities
* Integrate OpenShift with LDAP
* Integrate OpenShift with the Red Hat SSO OIDC (Keycloak)
* Manage multiple identity providers
* Configure authentication
* Configure and synchronize OpenShift groups
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

## Resolve synchronization conflicts

## Service accounts
Have this format: `system:serviceaccount:test:test-sa`

OpenShift contains default service accounts for cluster management, and generates the following service accounts for each project:

### builder
OpenShift uses this SA to build pods. By default, this SA has the system:image-builder role, so the resource can push images to any image stream in the project by using the internal Docker registry.

### deployer
OpenShift uses this SA in deployment pods. By default, this SA has the system:deployer role, so the resource can view and modify replication controllers and pods in the project. This SA exists only for applications that use OpenShift deployment configuration resources.

### default
OpenShift assigns this default SA to pods if you do not specify a different SA when you create the pods.




## OpenShift CLI Configuration Files

Include either a client certificate or an authentication token in a `kubeconfig` file. The kubeconfig file is defined as a YAML file that contains clusters, users, and contexts.

oc consumes:

1. The specified file in the --kubeconfig option, if you use it

2. The specified file in the KUBECONFIG environment variable, if it is set

3. The default ~/.kube/config file





