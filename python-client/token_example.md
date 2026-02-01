### How to use the Service account token to authenticate for python kubernetes client

Steps:
1. Create service account
  ```
  kubectl create serivceaccount <serviceaccountName>
  ```

2. Create rolebinding or clusterrolebinding for you service account
```
kubectl create clusterrolebinding <clusterrolebindingName> --clusterrole=cluster-admin --serviceaccount=namespace:serviceaccountname
```

3. Create secret of type service-aacount-token
```
apiVersion: v1
kind: Secret
metadata:
  name: sa-token-secret
  annotations:
    kubernetes.io/service-account.name: <serviceaccountName> #
type: kubernetes.io/service-account-token #

```

4. Get the token
   ```
   kubectl get secret sa-token-secret -o jsonpath='{.data.token}' | base64 --decode
   ```


```py
from kubernetes import client

# 1. Manually define your cluster details
TOKEN = "your_token_here" # kubectl get secret sa-token-secret -o jsonpath='{.data.token}' | base64 --decode
API_SERVER_URL = "https://172.30.1.2:6443" # kubectl config view (to get the server url)
CA_CERT_PATH = "/path/to/ca.crt" # Optional, for SSL verification

# 2. Setup the configuration
configuration = client.Configuration()
configuration.host = API_SERVER_URL
configuration.verify_ssl = False

# 3. Apply the token as a Bearer token
configuration.api_key["authorization"] = f"Bearer {TOKEN}"

# 4. Initialize the client with this configuration
api_client = client.ApiClient(configuration)
v1 = client.CoreV1Api(api_client)

# Example: List pods in the 'default' namespace
print("Listing pods:")
pods = v1.list_namespaced_pod(namespace="kube-system")
for pod in pods.items:
  print(f"- {pod.metadata.name}")
```


TroubleShooting
1. if the token is not working you can cross check the permissions using 
```
kubectl auth can-i --list --as=system:serviceaccount:<namespace>:<serviceaccount-name>
```
