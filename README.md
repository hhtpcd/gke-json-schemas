# gke-json-schemas

This is a collection of schemas for Google Kubernetes Engine. These can be
used with a tool like [kubeconform][kubeconform] to validate Kubernetes
resources. There are a number of other schemas included for utility controllers
that are not part of the core Kubernetes API.

Kubeconform already uses a number of inbuild Kubernetes schemas but it does
not have a way to validate custom schemas. This is a collection of Custom
Resource Definition schemas from Google Kubernetes Engine.

## Using the Schemas

```sh
kubeconform -schema-location 'default' \
    -schema-location 'https://raw.githubusercontent.com/hhtpcd/gke-json-schemas/master/{{ .ResourceKind }}_{{ .ResourceAPIVersion }}.json'
```

[kubeconform]: https://github.com/yannh/kubeconform