This role will create registries and projects in Harbor (using its REST API), which will serve as a proxy.

> You should use an Ansible vault to store your Harbor credentials !

Define the external registries you want to proxy using this variable :

```yaml
harbor_registries:
  - name: projects.registry.vmware.com
    url: https://projects.registry.vmware.com
    type: harbor
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
