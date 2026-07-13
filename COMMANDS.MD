helm install

helm install local-wp bitnami/wordpress

helm install local-wp bitnami/wordpress --set "mariadb.auth.rootPassword=mypass" --set "mariadb.auth.password=myuserpassword"

helm install local-wp bitnami/wordpress

### aplicar values.yaml

helm install local-wp bitnami/wordpress -f custom-values.yaml

helm get values local-wp

helm upgrade --reuse-values --values custom-values.yaml local-wp bitnami/wordpress --version=32.1.10

helm history local-wp

helm get values local-wp --revision 1

### Actualizar

helm repo update
helm search repo bitnami/wordpress --versions

### Rollback

helm upgrade --reuse-values --values custom-values.yaml --set "image.tag=nonexistent" local-wp bitnami/wordpress --version=32.1.10

helm rollback local-wp 3

not delete de rs when apply a rollback, we should delete manually

we will have as many secrets as we have upgrades/rollbacks

### Upgrading helm releases: Useful CLI flags

helm upgrade --reuse-values --values custom-values.yaml --set "image.tag=nonexistent" local-wp bitnami/wordpress --version=32.1.10 --atomic --cleanup-on-fail --debug --timeout 2m

helm history local-wp

helm get values local-wp --revision 9

the rs is not remove in a atomic rollback

what happens if I delete the secret state? of a previous version?

### Go templating

helm template .

## Package chart

This generate a tgz
helm package <nginx>
helm install local-nginx <tgx>

example:
helm install local-nginx nginx-0.1.0.tgz

helm repo index .

## Download chart

in the page (github page)
https://angeltravieso.github.io/helm-charts/index.yaml => this show the index.yaml of Chart
or
https://angeltravieso.github.io/helm-charts/nginx-0.1.0.tgz => this download the chart

## Install chart

helm repo add AngelTravieso <link github page>

example:

```
    helm repo add AngelTravieso https://angeltravieso.github.io/helm-charts/
```

Verify install of the repo

```
    helm repo list
```

Search for the Nginx chart

```
    helm search repo nginx
```

Install customize nginx chart

```
    helm install super-nginx AngelTravieso/nginx
```

Verify install of the Chart

```
    helm list
```

### Helm CLI for creating new charts

helm create <chart-name>
example:

```
    helm create backend-app
```
