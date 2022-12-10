This Ansible role will create registries and projects in Harbor (using its REST API), which will serve as a proxy cache.

:exclamation: You should use an Ansible vault to store your Harbor credentials !

Define the external registries you want to proxy using this variable :

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

As of Harbor 2.7.0, the registry types can be :
- `docker-hub`
- `docker-registry`
- `github-ghcr`
- `quay`
- `harbor`

For every registry, this Ansible role will create :
- a registry
- a "proxy cache" project.

Each project name will be suffixed with the "-proxy" tag (`quay.io-proxy` for example).
Projects will be public, and auto scan of CVEs will be enabled.

Projects storage limits are optional.
