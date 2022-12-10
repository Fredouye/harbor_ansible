This Ansible role will create registries and projects in Harbor (using its REST API), which will serve as a proxy cache.

:exclamation: You should use an Ansible vault to store your Harbor credentials !

Define the external registries you want to proxy using this list :

```yaml
harbor_registries:
  - name: projects.registry.vmware.com
    url: https://projects.registry.vmware.com
    type: harbor
    storage_limit: 10 GB
  - name: k8s.gcr.io
    url: https://k8s.gcr.io
    type: docker-registry
  - name: quay.io
    url: https://quay.io
    type: quay
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
