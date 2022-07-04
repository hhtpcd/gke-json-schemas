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

## Generating Schemas

Schemas are generated using `openapi2jsonschema` script in
[yannh/kubeconform][openapi2jsonschema]. It can be run against the CRDs from
a Kubernetes cluster or other OpenAPI schemas.

Retrieve active Custom Resource Definitions from a Kubernetes cluster. Useful
for unpublished Custom Resource Definitions from GKE clusters.

```sh
for CRD in $(kubectl get crds -o name); do \
    CRD_ESCAPED=$(echo ${CRD} | tr '/' '_')
    kubectl get ${CRD} -o json > "${CRD_ESCAPED}.json";
    openapi2jsonschema.py "${CRD_ESCAPED}.json"
done
```

Or retrieve a Custom Resource Definition from an open source project.

```sh
$ openapi2jsonschema.py  https://raw.githubusercontent.com/argoproj/argo-cd/master/manifests/crds/application-crd.yaml
JSON schema written to application_v1alpha1.json
```


[kubeconform]: https://github.com/yannh/kubeconform
[openapi2jsonschema]: https://github.com/yannh/kubeconform/tree/7bf1e01decc7e16c3a2d2388515e374d9629fd79/scripts