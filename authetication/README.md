# Authentication
**Authentication** konusuyla ilgili dosyalara buradan erişebilirsiniz.



**Key ve CSR oluşturma**
```
$ openssl genrsa -out mimaraslan.key 2048 

$ openssl req -new -key mimaraslan.key -out mimaraslan.csr -subj "/CN=mimar.aslan@gmail.com/O=DevTeam"
```

**CertificateSigningRequest oluşturma**

```
$ cat <<EOF | kubectl apply -f -
apiVersion: certificates.k8s.io/v1
kind: CertificateSigningRequest
metadata:
  name: mimaraslan
spec:
  groups:
  - system:authenticated
  request: $(cat mimaraslan.csr | base64 | tr -d "\n")
  signerName: kubernetes.io/kube-apiserver-client
  usages:
  - client auth
EOF
```

**CSR onaylama ve crt'yi alma**

```
$ kubectl get csr

$ kubectl certificate approve mimaraslan

$ kubectl get csr mimaraslan -o jsonpath='{.status.certificate}' | base64 -d >> mimaraslan.crt 
```

**kubectl config ayarları**

```
$ kubectl config set-credentials mimaraslan --client-certificate=mimaraslan.crt --client-key=mimaraslan.key

$ kubectl config set-context mimaraslan-context --cluster=minikube --user=mimar.aslan@gmail.com

$ kubectl config use-context mimaraslan-context
```