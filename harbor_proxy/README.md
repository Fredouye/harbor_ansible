This Ansible role will create registries and projects in Harbor (using its REST API), which will serve as a proxy cache.

:exclamation: You should use an Ansible vault to store your Harbor credentials !

Firstly, define your Harbor instance :

```yaml
harbor_url: https://harbor.foo.com
harbor_username: my-admin-username
harbor_password: my-admin-password
```

If you're using a self signed TLS certificate, set this variable to `false` :

```yaml
check_tls_certificate: false
```

If this variable is not set, TLS certificate will be checked.

Define the external registries you want to proxy using this list :

```yaml
harbor_registries:
  - name: docker.io
    url: https://hub.docker.com
    type: docker-hub
  - name: gcr.io
    url: https://gcr.io
    type: docker-registry
    storage_limit: 1 GB
  - name: registry.k8s.io
    url: https://registry.k8s.io
    type: docker-registry
    storage_limit: 2 GB
  - name: quay.io
    url: https://quay.io
    type: quay
    storage_limit: 1 GB
  - name: ghcr.io
    url: https://ghcr.io
    type: github-ghcr
    storage_limit: 1 GB
```

As of Harbor 2.7.0, common types of registries are :
- `docker-hub`
- `docker-registry`
- `github-ghcr`
- `quay`
- `harbor`

For every external registry, this role will create :
- a registry (`quay.io` for example)
- a "proxy cache" project (`quay.io-proxy` for example).

Projects storage limits (`2GB` for example) are optional.
