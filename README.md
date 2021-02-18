### k8s-cli-utils (namespace:default)
Docker image that has kubectl, kube-aws and helm tools pre-installed.

#### Build locally
```
docker build -t davarski/k8s-cli-utils:local .

```

#### Running locally

Expected environment variables:

- K8S_API_SERVER: the URL of the API server of the Kubernetes cluster
- K8S_TOKEN: For authentication with the K8s API server, it uses [service account tokens](https://kubernetes.io/docs/admin/authentication/#service-account-tokens). This is the token of the service account.

#### Usage 
Start the container with an interactive tools i.e. sh:
```
docker run -it --rm -e "K8S_API_SERVER=<k8s-api-server-url>" -e "K8S_TOKEN=<the_token>" davarski/k8s-cli-utils:local /bin/sh
```
#### Example

```
$ kubectl create serviceaccount k8s-user

$ kubectl create rolebinding k8s-user --clusterrole=cluster-admin --serviceaccount=default:k8s-user

$ kubectl get serviceaccounts k8s-user -o yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  creationTimestamp: "2021-02-18T09:03:11Z"
  name: k8s-user
  namespace: default
  resourceVersion: "4494639"
  selfLink: /api/v1/namespaces/default/serviceaccounts/k8s-user
  uid: e4b7e0e6-30cf-4dc3-9d94-6cfe84989290
secrets:
- name: k8s-user-token-tgkqg

$ kubectl get secret k8s-user-token-tgkqg -o yaml
apiVersion: v1
data:
  ca.crt: LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSUJkekNDQVIyZ0F3SUJBZ0lCQURBS0JnZ3Foa2pPUFFRREFqQWpNU0V3SHdZRFZRUUREQmhyTTNNdGMyVnkKZG1WeUxXTmhRREUyTURVNE5USXhOemN3SGhjTk1qQXhNVEl3TURZd01qVTNXaGNOTXpBeE1URTRNRFl3TWpVMwpXakFqTVNFd0h3WURWUVFEREJock0zTXRjMlZ5ZG1WeUxXTmhRREUyTURVNE5USXhOemN3V1RBVEJnY3Foa2pPClBRSUJCZ2dxaGtqT1BRTUJCd05DQUFSMkNMVzZkSEs0UnVmLzJRaWNvd0JtNFJ6SVJJK3lTSlZ6TlhWSHRtR1YKbzRFWml3Z3JOQnBzK2tlNkhscUJlSzVWQlArTjVHYmp2SE9LZUM2U3NJOFJvMEl3UURBT0JnTlZIUThCQWY4RQpCQU1DQXFRd0R3WURWUjBUQVFIL0JBVXdBd0VCL3pBZEJnTlZIUTRFRmdRVWgvdkUwQVlXa3ZqTGdXcUYwZWNTCjZOZEp1SjB3Q2dZSUtvWkl6ajBFQXdJRFNBQXdSUUloQUpmK0J6d2JTaDBiaTdldEpIQlppRzdXaG9PaUNHaEUKcVMzTUhXQXhsWm1GQWlBSDIwYzhPUnFkbElSYnJ0Y0paMlpHdGw1Wk5aMnNNUW9LNENoa01IQlBoUT09Ci0tLS0tRU5EIENFUlRJRklDQVRFLS0tLS0K
  namespace: ZGVmYXVsdA==
  token: ZXlKaGJHY2lPaUpTVXpJMU5pSXNJbXRwWkNJNklrOW9kR2hmU0hSelExTmlNMVpRU1ZSUVpsUTJOVUpRUkRGVk4yRk1PVk5JV1ZwRldTMTVWa3R2VFhNaWZRLmV5SnBjM01pT2lKcmRXSmxjbTVsZEdWekwzTmxjblpwWTJWaFkyTnZkVzUwSWl3aWEzVmlaWEp1WlhSbGN5NXBieTl6WlhKMmFXTmxZV05qYjNWdWRDOXVZVzFsYzNCaFkyVWlPaUprWldaaGRXeDBJaXdpYTNWaVpYSnVaWFJsY3k1cGJ5OXpaWEoyYVdObFlXTmpiM1Z1ZEM5elpXTnlaWFF1Ym1GdFpTSTZJbXM0Y3kxMWMyVnlMWFJ2YTJWdUxYUm5hM0ZuSWl3aWEzVmlaWEp1WlhSbGN5NXBieTl6WlhKMmFXTmxZV05qYjNWdWRDOXpaWEoyYVdObExXRmpZMjkxYm5RdWJtRnRaU0k2SW1zNGN5MTFjMlZ5SWl3aWEzVmlaWEp1WlhSbGN5NXBieTl6WlhKMmFXTmxZV05qYjNWdWRDOXpaWEoyYVdObExXRmpZMjkxYm5RdWRXbGtJam9pWlRSaU4yVXdaVFl0TXpCalppMDBaR016TFRsa09UUXRObU5tWlRnME9UZzVNamt3SWl3aWMzVmlJam9pYzNsemRHVnRPbk5sY25acFkyVmhZMk52ZFc1ME9tUmxabUYxYkhRNmF6aHpMWFZ6WlhJaWZRLmlOU3lKWnA2MlNwVGhxTnhhQVlReC1PQ1FqdWw1YU5qOUJycVhZWTlvOWh1MF9BcXJSQW1EQk5TSlRXRGVLckxOdzE5T2NBREhZMXFWSHAwVks0ZWdReHhxcTVUN016M3RORnI4dldEVUlRUWxwZXdlX1AxNHlPMWJKTE0zMUhCWXJyc2pWd2Vpb3JHSHJqdm1vbkVlLTYxZnpoWTVkdDdrb05HTm96aTRHNjI5R09kX1pUYVA3U3F0SU9YSkpEQ0NocXJMZFJtRWtTOEpoc2tnT2g3allpSjlmbDBTMTQxcWt5d1BsQUhvVEpYMFlzVTlGbUF0VGJzUVJBS2sxN1BBblVJeTBmeFE2WktCN0FEeDJtRFBRN1VhSFV4bTlpOHY4MmtiNjdPcVJpX2x5bzdTdndQVzF6Wm91Nkh1ZVFGeTlHUnNRSlI5b1R3azgwYzY1N2RzUQ==
kind: Secret
metadata:
  annotations:
    kubernetes.io/service-account.name: k8s-user
    kubernetes.io/service-account.uid: e4b7e0e6-30cf-4dc3-9d94-6cfe84989290
  creationTimestamp: "2021-02-18T09:03:11Z"
  managedFields:
  - apiVersion: v1
    fieldsType: FieldsV1
    fieldsV1:
      f:data:
        .: {}
        f:ca.crt: {}
        f:namespace: {}
        f:token: {}
      f:metadata:
        f:annotations:
          .: {}
          f:kubernetes.io/service-account.name: {}
          f:kubernetes.io/service-account.uid: {}
      f:type: {}
    manager: k3s
    operation: Update
    time: "2021-02-18T09:03:11Z"
  name: k8s-user-token-tgkqg
  namespace: default
  resourceVersion: "4494638"
  selfLink: /api/v1/namespaces/default/secrets/k8s-user-token-tgkqg
  uid: d3892ac7-fe26-4235-968d-9eca22a5a0c6
type: kubernetes.io/service-account-token

$ echo "ZXlKaGJHY2lPaUpTVXpJMU5pSXNJbXRwWkNJNklrOW9kR2hmU0hSelExTmlNMVpRU1ZSUVpsUTJOVUpRUkRGVk4yRk1PVk5JV1ZwRldTMTVWa3R2VFhNaWZRLmV5SnBjM01pT2lKcmRXSmxjbTVsZEdWekwzTmxjblpwWTJWaFkyTnZkVzUwSWl3aWEzVmlaWEp1WlhSbGN5NXBieTl6WlhKMmFXTmxZV05qYjNWdWRDOXVZVzFsYzNCaFkyVWlPaUprWldaaGRXeDBJaXdpYTNWaVpYSnVaWFJsY3k1cGJ5OXpaWEoyYVdObFlXTmpiM1Z1ZEM5elpXTnlaWFF1Ym1GdFpTSTZJbXM0Y3kxMWMyVnlMWFJ2YTJWdUxYUm5hM0ZuSWl3aWEzVmlaWEp1WlhSbGN5NXBieTl6WlhKMmFXTmxZV05qYjNWdWRDOXpaWEoyYVdObExXRmpZMjkxYm5RdWJtRnRaU0k2SW1zNGN5MTFjMlZ5SWl3aWEzVmlaWEp1WlhSbGN5NXBieTl6WlhKMmFXTmxZV05qYjNWdWRDOXpaWEoyYVdObExXRmpZMjkxYm5RdWRXbGtJam9pWlRSaU4yVXdaVFl0TXpCalppMDBaR016TFRsa09UUXRObU5tWlRnME9UZzVNamt3SWl3aWMzVmlJam9pYzNsemRHVnRPbk5sY25acFkyVmhZMk52ZFc1ME9tUmxabUYxYkhRNmF6aHpMWFZ6WlhJaWZRLmlOU3lKWnA2MlNwVGhxTnhhQVlReC1PQ1FqdWw1YU5qOUJycVhZWTlvOWh1MF9BcXJSQW1EQk5TSlRXRGVLckxOdzE5T2NBREhZMXFWSHAwVks0ZWdReHhxcTVUN016M3RORnI4dldEVUlRUWxwZXdlX1AxNHlPMWJKTE0zMUhCWXJyc2pWd2Vpb3JHSHJqdm1vbkVlLTYxZnpoWTVkdDdrb05HTm96aTRHNjI5R09kX1pUYVA3U3F0SU9YSkpEQ0NocXJMZFJtRWtTOEpoc2tnT2g3allpSjlmbDBTMTQxcWt5d1BsQUhvVEpYMFlzVTlGbUF0VGJzUVJBS2sxN1BBblVJeTBmeFE2WktCN0FEeDJtRFBRN1VhSFV4bTlpOHY4MmtiNjdPcVJpX2x5bzdTdndQVzF6Wm91Nkh1ZVFGeTlHUnNRSlI5b1R3azgwYzY1N2RzUQ=="|base64 -d
eyJhbGciOiJSUzI1NiIsImtpZCI6Ik9odGhfSHRzQ1NiM1ZQSVRQZlQ2NUJQRDFVN2FMOVNIWVpFWS15VktvTXMifQ.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJkZWZhdWx0Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZWNyZXQubmFtZSI6Ims4cy11c2VyLXRva2VuLXRna3FnIiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZXJ2aWNlLWFjY291bnQubmFtZSI6Ims4cy11c2VyIiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZXJ2aWNlLWFjY291bnQudWlkIjoiZTRiN2UwZTYtMzBjZi00ZGMzLTlkOTQtNmNmZTg0OTg5MjkwIiwic3ViIjoic3lzdGVtOnNlcnZpY2VhY2NvdW50OmRlZmF1bHQ6azhzLXVzZXIifQ.iNSyJZp62SpThqNxaAYQx-OCQjul5aNj9BrqXYY9o9hu0_AqrRAmDBNSJTWDeKrLNw19OcADHY1qVHp0VK4egQxxqq5T7Mz3tNFr8vWDUIQQlpewe_P14yO1bJLM31HBYrrsjVweiorGHrjvmonEe-61fzhY5dt7koNGNozi4G629GOd_ZTaP7SqtIOXJJDCChqrLdRmEkS8JhskgOh7jYiJ9fl0S141qkywPlAHoTJX0YsU9FmAtTbsQRAKk17PAnUIy0fxQ6ZKB7ADx2mDPQ7UaHUxm9i8v82kb67OqRi_lyo7SvwPW1zZou6HueQFy9GRsQJR9oTwk80c657dsQ 
$ docker run -it --rm -e "K8S_API_SERVER=https://192.168.0.105:6443" -e "K8S_TOKEN=eyJhbGciOiJSUzI1NiIsImtpZCI6Ik9odGhfSHRzQ1NiM1ZQSVRQZlQ2NUJQRDFVN2FMOVNIWVpFWS15VktvTXMifQ.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJkZWZhdWx0Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZWNyZXQubmFtZSI6Ims4cy11c2VyLXRva2VuLXRna3FnIiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZXJ2aWNlLWFjY291bnQubmFtZSI6Ims4cy11c2VyIiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZXJ2aWNlLWFjY291bnQudWlkIjoiZTRiN2UwZTYtMzBjZi00ZGMzLTlkOTQtNmNmZTg0OTg5MjkwIiwic3ViIjoic3lzdGVtOnNlcnZpY2VhY2NvdW50OmRlZmF1bHQ6azhzLXVzZXIifQ.iNSyJZp62SpThqNxaAYQx-OCQjul5aNj9BrqXYY9o9hu0_AqrRAmDBNSJTWDeKrLNw19OcADHY1qVHp0VK4egQxxqq5T7Mz3tNFr8vWDUIQQlpewe_P14yO1bJLM31HBYrrsjVweiorGHrjvmonEe-61fzhY5dt7koNGNozi4G629GOd_ZTaP7SqtIOXJJDCChqrLdRmEkS8JhskgOh7jYiJ9fl0S141qkywPlAHoTJX0YsU9FmAtTbsQRAKk17PAnUIy0fxQ6ZKB7ADx2mDPQ7UaHUxm9i8v82kb67OqRi_lyo7SvwPW1zZou6HueQFy9GRsQJR9oTwk80c657dsQ" davarski/k8s-cli-utils:local /bin/sh
/ # kubectl get po
NAME               READY   STATUS    RESTARTS   AGE
jupyter-notebook   1/1     Running   55         40d
busybox            1/1     Running   998        89d
dnsutils           1/1     Running   994        88d

/ # helm list
WARNING: Kubernetes configuration file is group-readable. This is insecure. Location: /kubeconfig
WARNING: Kubernetes configuration file is world-readable. This is insecure. Location: /kubeconfig
NAME	NAMESPACE	REVISION	UPDATED	STATUS	CHART	APP VERSION


/ # kubectl get po -n data
Error from server (Forbidden): pods is forbidden: User "system:serviceaccount:default:k8s-user" cannot list resource "pods" in API group "" in the namespace "data"

/ # helm list -n data
WARNING: Kubernetes configuration file is group-readable. This is insecure. Location: /kubeconfig
WARNING: Kubernetes configuration file is world-readable. This is insecure. Location: /kubeconfig
Error: list: failed to list: secrets is forbidden: User "system:serviceaccount:default:k8s-user" cannot list resource "secrets" in API group "" in the namespace "data"

# env
HOSTNAME=f247617bf57c
SHLVL=2
HOME=/root
HELM_DLD_TEMP_LOCATION=helm.tar.gz
KUBE_AWS_VERSION=v0.12.2
TERM=xterm
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
K8S_TOKEN=eyJhbGciOiJSUzI1NiIsImtpZCI6Ik9odGhfSHRzQ1NiM1ZQSVRQZlQ2NUJQRDFVN2FMOVNIWVpFWS15VktvTXMifQ.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJkZWZhdWx0Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZWNyZXQubmFtZSI6Ims4cy11c2VyLXRva2VuLXRna3FnIiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZXJ2aWNlLWFjY291bnQubmFtZSI6Ims4cy11c2VyIiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZXJ2aWNlLWFjY291bnQudWlkIjoiZTRiN2UwZTYtMzBjZi00ZGMzLTlkOTQtNmNmZTg0OTg5MjkwIiwic3ViIjoic3lzdGVtOnNlcnZpY2VhY2NvdW50OmRlZmF1bHQ6azhzLXVzZXIifQ.iNSyJZp62SpThqNxaAYQx-OCQjul5aNj9BrqXYY9o9hu0_AqrRAmDBNSJTWDeKrLNw19OcADHY1qVHp0VK4egQxxqq5T7Mz3tNFr8vWDUIQQlpewe_P14yO1bJLM31HBYrrsjVweiorGHrjvmonEe-61fzhY5dt7koNGNozi4G629GOd_ZTaP7SqtIOXJJDCChqrLdRmEkS8JhskgOh7jYiJ9fl0S141qkywPlAHoTJX0YsU9FmAtTbsQRAKk17PAnUIy0fxQ6ZKB7ADx2mDPQ7UaHUxm9i8v82kb67OqRi_lyo7SvwPW1zZou6HueQFy9GRsQJR9oTwk80c657dsQ
KUBECONFIG=/kubeconfig
HELM_VERSION=v3.4.1
KUBECTL_VERSION=v1.19.3
K8S_API_SERVER=https://192.168.0.105:6443
PWD=/
KUBE_AWS_DLD_TEMP_LOCATION=kube-aws.tar.gz

/ # cat kubeconfig
apiVersion: v1
kind: Config
clusters:
- cluster:
    # Skip TLS verification instead of passing in the CA of the API server.
    insecure-skip-tls-verify: true
    server: https://192.168.0.105:6443
  name: k8s-cluster
contexts:
- context:
    cluster: k8s-cluster
    namespace: default
    user: k8s-user
  name: k8s-context
users:
- name: k8s-user
  user:
    token: eyJhbGciOiJSUzI1NiIsImtpZCI6Ik9odGhfSHRzQ1NiM1ZQSVRQZlQ2NUJQRDFVN2FMOVNIWVpFWS15VktvTXMifQ.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJkZWZhdWx0Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZWNyZXQubmFtZSI6Ims4cy11c2VyLXRva2VuLXRna3FnIiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZXJ2aWNlLWFjY291bnQubmFtZSI6Ims4cy11c2VyIiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZXJ2aWNlLWFjY291bnQudWlkIjoiZTRiN2UwZTYtMzBjZi00ZGMzLTlkOTQtNmNmZTg0OTg5MjkwIiwic3ViIjoic3lzdGVtOnNlcnZpY2VhY2NvdW50OmRlZmF1bHQ6azhzLXVzZXIifQ.iNSyJZp62SpThqNxaAYQx-OCQjul5aNj9BrqXYY9o9hu0_AqrRAmDBNSJTWDeKrLNw19OcADHY1qVHp0VK4egQxxqq5T7Mz3tNFr8vWDUIQQlpewe_P14yO1bJLM31HBYrrsjVweiorGHrjvmonEe-61fzhY5dt7koNGNozi4G629GOd_ZTaP7SqtIOXJJDCChqrLdRmEkS8JhskgOh7jYiJ9fl0S141qkywPlAHoTJX0YsU9FmAtTbsQRAKk17PAnUIy0fxQ6ZKB7ADx2mDPQ7UaHUxm9i8v82kb67OqRi_lyo7SvwPW1zZou6HueQFy9GRsQJR9oTwk80c657dsQ
current-context: k8s-context
```
### k8s-cli-utils (RBAC; namespace: development)

#### Build locally
```
cd k8s-RBAC
docker build -t davarski/k8s-cli-utils:development .
```
#### Running locally

Expected environment variables:

- K8S_API_SERVER: the URL of the API server of the Kubernetes cluster
- K8S_TOKEN: For authentication with the K8s API server, it uses [service account tokens](https://kubernetes.io/docs/admin/authentication/#service-account-tokens). This is the token of the service account.

#### Usage 
Start the container with an interactive tools i.e. sh:
```
docker run -it --rm -e "K8S_API_SERVER=<k8s-api-server-url>" -e "K8S_TOKEN=<the_token>" davarski/k8s-cli-utils:development /bin/sh
```



Example:
```
$ kubectl apply -f 00-namespace.yml -f 05-serviceaccount.yml -f 07-role.yml -f 08-rolebinding.yml
$ kubectl get serviceaccounts k8s-user -n development -o yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"v1","kind":"ServiceAccount","metadata":{"annotations":{},"name":"k8s-user","namespace":"development"}}
  creationTimestamp: "2021-02-18T09:47:37Z"
  managedFields:
  - apiVersion: v1
    fieldsType: FieldsV1
    fieldsV1:
      f:secrets:
        .: {}
        k:{"name":"k8s-user-token-69t8m"}:
          .: {}
          f:name: {}
    manager: k3s
    operation: Update
    time: "2021-02-18T09:47:37Z"
  - apiVersion: v1
    fieldsType: FieldsV1
    fieldsV1:
      f:metadata:
        f:annotations:
          .: {}
          f:kubectl.kubernetes.io/last-applied-configuration: {}
    manager: kubectl-client-side-apply
    operation: Update
    time: "2021-02-18T09:47:37Z"
  name: k8s-user
  namespace: development
  resourceVersion: "4498085"
  selfLink: /api/v1/namespaces/development/serviceaccounts/k8s-user
  uid: 22b8804f-b821-4ce7-82f3-d34b6a571754
secrets:
- name: k8s-user-token-69t8m

$ kubectl get secret k8s-user-token-69t8m -n development -o yaml
apiVersion: v1
data:
  ca.crt: LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSUJkekNDQVIyZ0F3SUJBZ0lCQURBS0JnZ3Foa2pPUFFRREFqQWpNU0V3SHdZRFZRUUREQmhyTTNNdGMyVnkKZG1WeUxXTmhRREUyTURVNE5USXhOemN3SGhjTk1qQXhNVEl3TURZd01qVTNXaGNOTXpBeE1URTRNRFl3TWpVMwpXakFqTVNFd0h3WURWUVFEREJock0zTXRjMlZ5ZG1WeUxXTmhRREUyTURVNE5USXhOemN3V1RBVEJnY3Foa2pPClBRSUJCZ2dxaGtqT1BRTUJCd05DQUFSMkNMVzZkSEs0UnVmLzJRaWNvd0JtNFJ6SVJJK3lTSlZ6TlhWSHRtR1YKbzRFWml3Z3JOQnBzK2tlNkhscUJlSzVWQlArTjVHYmp2SE9LZUM2U3NJOFJvMEl3UURBT0JnTlZIUThCQWY4RQpCQU1DQXFRd0R3WURWUjBUQVFIL0JBVXdBd0VCL3pBZEJnTlZIUTRFRmdRVWgvdkUwQVlXa3ZqTGdXcUYwZWNTCjZOZEp1SjB3Q2dZSUtvWkl6ajBFQXdJRFNBQXdSUUloQUpmK0J6d2JTaDBiaTdldEpIQlppRzdXaG9PaUNHaEUKcVMzTUhXQXhsWm1GQWlBSDIwYzhPUnFkbElSYnJ0Y0paMlpHdGw1Wk5aMnNNUW9LNENoa01IQlBoUT09Ci0tLS0tRU5EIENFUlRJRklDQVRFLS0tLS0K
  namespace: ZGV2ZWxvcG1lbnQ=
  token: ZXlKaGJHY2lPaUpTVXpJMU5pSXNJbXRwWkNJNklrOW9kR2hmU0hSelExTmlNMVpRU1ZSUVpsUTJOVUpRUkRGVk4yRk1PVk5JV1ZwRldTMTVWa3R2VFhNaWZRLmV5SnBjM01pT2lKcmRXSmxjbTVsZEdWekwzTmxjblpwWTJWaFkyTnZkVzUwSWl3aWEzVmlaWEp1WlhSbGN5NXBieTl6WlhKMmFXTmxZV05qYjNWdWRDOXVZVzFsYzNCaFkyVWlPaUprWlhabGJHOXdiV1Z1ZENJc0ltdDFZbVZ5Ym1WMFpYTXVhVzh2YzJWeWRtbGpaV0ZqWTI5MWJuUXZjMlZqY21WMExtNWhiV1VpT2lKck9ITXRkWE5sY2kxMGIydGxiaTAyT1hRNGJTSXNJbXQxWW1WeWJtVjBaWE11YVc4dmMyVnlkbWxqWldGalkyOTFiblF2YzJWeWRtbGpaUzFoWTJOdmRXNTBMbTVoYldVaU9pSnJPSE10ZFhObGNpSXNJbXQxWW1WeWJtVjBaWE11YVc4dmMyVnlkbWxqWldGalkyOTFiblF2YzJWeWRtbGpaUzFoWTJOdmRXNTBMblZwWkNJNklqSXlZamc0TURSbUxXSTRNakV0TkdObE55MDRNbVl6TFdRek5HSTJZVFUzTVRjMU5DSXNJbk4xWWlJNkluTjVjM1JsYlRwelpYSjJhV05sWVdOamIzVnVkRHBrWlhabGJHOXdiV1Z1ZERwck9ITXRkWE5sY2lKOS5IWEw5N2NiR21scHhlbTd4ZkxBeVh3RXplYjJjLWRsR2VscXNCT1haR0lOUGRWdHlEN0pfUlN3UERnMDVlUEFXOVEtbjFjcFV5SE54UldESUR0V3VILUFOZzZHcGRlVWd3S0FIZndOcVpnTEFDOTZ3Zjl0bFlMUEcwSVZ6aU1nWW5xc0pKeGg0bVd5SlZodjN0eDNOV2xmdTNaYlNaVjNpNmFTdklHSm5fZHJ1YzdmRGZIb2JmTHNicV90VjlLaDU3aFRNXzlfYlFIbndIXzgyckE2eUxXZVpQYnlUcThaRVU3Q09yQWtKTGhLUWMxQWw2ckItM2lHdzBHRVo0Y1E5MURjRmxuSHJXRXpHUVJ0ODRSal9BQUxFYVk3dlV0THlGSTNVWHVEYjBvd3d0YWUyVm13S2ZfcWFONGREV0NDUTdvMEZtWE1mVTY1Szktbm9ZcmNfbFE=
kind: Secret
metadata:
  annotations:
    kubernetes.io/service-account.name: k8s-user
    kubernetes.io/service-account.uid: 22b8804f-b821-4ce7-82f3-d34b6a571754
  creationTimestamp: "2021-02-18T09:47:37Z"
  managedFields:
  - apiVersion: v1
    fieldsType: FieldsV1
    fieldsV1:
      f:data:
        .: {}
        f:ca.crt: {}
        f:namespace: {}
        f:token: {}
      f:metadata:
        f:annotations:
          .: {}
          f:kubernetes.io/service-account.name: {}
          f:kubernetes.io/service-account.uid: {}
      f:type: {}
    manager: k3s
    operation: Update
    time: "2021-02-18T09:47:37Z"
  name: k8s-user-token-69t8m
  namespace: development
  resourceVersion: "4498084"
  selfLink: /api/v1/namespaces/development/secrets/k8s-user-token-69t8m
  uid: 2032acae-4e6e-446a-8646-a5885ea23d81
type: kubernetes.io/service-account-token

$ echo "ZXlKaGJHY2lPaUpTVXpJMU5pSXNJbXRwWkNJNklrOW9kR2hmU0hSelExTmlNMVpRU1ZSUVpsUTJOVUpRUkRGVk4yRk1PVk5JV1ZwRldTMTVWa3R2VFhNaWZRLmV5SnBjM01pT2lKcmRXSmxjbTVsZEdWekwzTmxjblpwWTJWaFkyTnZkVzUwSWl3aWEzVmlaWEp1WlhSbGN5NXBieTl6WlhKMmFXTmxZV05qYjNWdWRDOXVZVzFsYzNCaFkyVWlPaUprWlhabGJHOXdiV1Z1ZENJc0ltdDFZbVZ5Ym1WMFpYTXVhVzh2YzJWeWRtbGpaV0ZqWTI5MWJuUXZjMlZqY21WMExtNWhiV1VpT2lKck9ITXRkWE5sY2kxMGIydGxiaTAyT1hRNGJTSXNJbXQxWW1WeWJtVjBaWE11YVc4dmMyVnlkbWxqWldGalkyOTFiblF2YzJWeWRtbGpaUzFoWTJOdmRXNTBMbTVoYldVaU9pSnJPSE10ZFhObGNpSXNJbXQxWW1WeWJtVjBaWE11YVc4dmMyVnlkbWxqWldGalkyOTFiblF2YzJWeWRtbGpaUzFoWTJOdmRXNTBMblZwWkNJNklqSXlZamc0TURSbUxXSTRNakV0TkdObE55MDRNbVl6TFdRek5HSTJZVFUzTVRjMU5DSXNJbk4xWWlJNkluTjVjM1JsYlRwelpYSjJhV05sWVdOamIzVnVkRHBrWlhabGJHOXdiV1Z1ZERwck9ITXRkWE5sY2lKOS5IWEw5N2NiR21scHhlbTd4ZkxBeVh3RXplYjJjLWRsR2VscXNCT1haR0lOUGRWdHlEN0pfUlN3UERnMDVlUEFXOVEtbjFjcFV5SE54UldESUR0V3VILUFOZzZHcGRlVWd3S0FIZndOcVpnTEFDOTZ3Zjl0bFlMUEcwSVZ6aU1nWW5xc0pKeGg0bVd5SlZodjN0eDNOV2xmdTNaYlNaVjNpNmFTdklHSm5fZHJ1YzdmRGZIb2JmTHNicV90VjlLaDU3aFRNXzlfYlFIbndIXzgyckE2eUxXZVpQYnlUcThaRVU3Q09yQWtKTGhLUWMxQWw2ckItM2lHdzBHRVo0Y1E5MURjRmxuSHJXRXpHUVJ0ODRSal9BQUxFYVk3dlV0THlGSTNVWHVEYjBvd3d0YWUyVm13S2ZfcWFONGREV0NDUTdvMEZtWE1mVTY1Szktbm9ZcmNfbFE="|base64 -d
eyJhbGciOiJSUzI1NiIsImtpZCI6Ik9odGhfSHRzQ1NiM1ZQSVRQZlQ2NUJQRDFVN2FMOVNIWVpFWS15VktvTXMifQ.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJkZXZlbG9wbWVudCIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VjcmV0Lm5hbWUiOiJrOHMtdXNlci10b2tlbi02OXQ4bSIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VydmljZS1hY2NvdW50Lm5hbWUiOiJrOHMtdXNlciIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VydmljZS1hY2NvdW50LnVpZCI6IjIyYjg4MDRmLWI4MjEtNGNlNy04MmYzLWQzNGI2YTU3MTc1NCIsInN1YiI6InN5c3RlbTpzZXJ2aWNlYWNjb3VudDpkZXZlbG9wbWVudDprOHMtdXNlciJ9.HXL97cbGmlpxem7xfLAyXwEzeb2c-dlGelqsBOXZGINPdVtyD7J_RSwPDg05ePAW9Q-n1cpUyHNxRWDIDtWuH-ANg6GpdeUgwKAHfwNqZgLAC96wf9tlYLPG0IVziMgYnqsJJxh4mWyJVhv3tx3NWlfu3ZbSZV3i6aSvIGJn_druc7fDfHobfLsbq_tV9Kh57hTM_9_bQHnwH_82rA6yLWeZPbyTq8ZEU7COrAkJLhKQc1Al6rB-3iGw0GEZ4cQ91DcFlnHrWEzGQRt84Rj_AALEaY7vUtLyFI3UXuDb0owwtae2VmwKf_qaN4dDWCCQ7o0FmXMfU65K9-noYrc_lQ

$ docker run -it --rm -e "K8S_API_SERVER=https://192.168.0.105:6443" -e "K8S_TOKEN=eyJhbGcSUzI1NiIsImtpZCI6Ik9odGhfSHRzQ1NiM1ZQSVRQZlQ2NUJQRDFVN2FMOVNIWVpFWS15VktvTXMifQ.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJkZXZlbG9wbWVudCIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VjcmV0Lm5hbWUiOiJrOHMtdXNlci10b2tlbi02OXQ4bSIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VydmljZS1hY2NvdW50Lm5hbWUiOiJrOHMtdXNlciIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VydmljZS1hY2NvdW50LnVpZCI6IjIyYjg4MDRmLWI4MjEtNGNlNy04MmYzLWQzNGI2YTU3MTc1NCIsInN1YiI6InN5c3RlbTpzZXJ2aWNlYWNjb3VudDpkZXZlbG9wbWVudDprOHMtdXNlciJ9.HXL97cbGmlpxem7xfLAyXwEzeb2c-dlGelqsBOXZGINPdVtyD7J_RSwPDg05ePAW9Q-n1cpUyHNxRWDIDtWuH-ANg6GpdeUgwKAHfwNqZgLAC96wf9tlYLPG0IVziMgYnqsJJxh4mWyJVhv3tx3NWlfu3ZbSZV3i6aSvIGJn_druc7fDfHobfLsbq_tV9Kh57hTM_9_bQHnwH_82rA6yLWeZPbyTq8ZEU7COrAkJLhKQc1Al6rB-3iGw0GEZ4cQ91DcFlnHrWEzGQRt84Rj_AALEaY7vUtLyFI3UXuDb0owwtae2VmwKf_qaN4dDWCCQ7o0FmXMfU65K9-noYrc_lQ" davarski/k8s-cli-utils:development /bin/sh

/ # kubectl get po
No resources found in development namespace.

/ # kubectl run nginx --image=nginx --port=80 -n development
pod/nginx created

/ # kubectl get po
NAME    READY   STATUS    RESTARTS   AGE
nginx   1/1     Running   0          2m1s

/ # kubectl get all -n development
NAME        READY   STATUS              RESTARTS   AGE
pod/nginx   0/1     ContainerCreating   0          86s
Error from server (Forbidden): replicationcontrollers is forbidden: User "system:serviceaccount:development:k8s-user" cannot list resource "replicationcontrollers" in API group "" in the namespace "development"
Error from server (Forbidden): daemonsets.apps is forbidden: User "system:serviceaccount:development:k8s-user" cannot list resource "daemonsets" in API group "apps" in the namespace "development"
Error from server (Forbidden): deployments.apps is forbidden: User "system:serviceaccount:development:k8s-user" cannot list resource "deployments" in API group "apps" in the namespace "development"
Error from server (Forbidden): replicasets.apps is forbidden: User "system:serviceaccount:development:k8s-user" cannot list resource "replicasets" in API group "apps" in the namespace "development"
Error from server (Forbidden): statefulsets.apps is forbidden: User "system:serviceaccount:development:k8s-user" cannot list resource "statefulsets" in API group "apps" in the namespace "development"
Error from server (Forbidden): horizontalpodautoscalers.autoscaling is forbidden: User "system:serviceaccount:development:k8s-user" cannot list resource "horizontalpodautoscalers" in API group "autoscaling" in the namespace "development"
Error from server (Forbidden): jobs.batch is forbidden: User "system:serviceaccount:development:k8s-user" cannot list resource "jobs" in API group "batch" in the namespace "development"
Error from server (Forbidden): cronjobs.batch is forbidden: User "system:serviceaccount:development:k8s-user" cannot list resource "cronjobs" in API group "batch" in the namespace "development"
/ # 

#Clean

$ kubectl delete -f 00-namespace.yml -f 05-serviceaccount.yml -f 07-role.yml -f 08-rolebinding.yml
namespace "development" deleted
serviceaccount "k8s-user" deleted
Warning: rbac.authorization.k8s.io/v1beta1 Role is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 Role
role.rbac.authorization.k8s.io "k8s-user" deleted
Warning: rbac.authorization.k8s.io/v1beta1 RoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 RoleBinding
rolebinding.rbac.authorization.k8s.io "k8s-user" deleted

```
