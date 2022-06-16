# ImageSecret
**ImageSecret** konusuyla ilgili dosyalara buradan erişebilirsiniz.
***
Authetication gerektiren bir Docker registry'den image çekebilmek için oluşturulması gereken secret'in oluşturulması

```
$ kubectl create secret docker-registry "secret_ismi" --docker-server="registry_url" --docker-username="kullanıcı_adı" --docker-password="şifre"

Ör: kubectl create secret docker-registry regscrt --docker-server=mimaraslanregistry.azurecr.io --docker-username=mimaraslanregistry --docker-password=wqRjEDdVhrM9Hj4D=gWwvV3YXyq9Y4ID
```
***