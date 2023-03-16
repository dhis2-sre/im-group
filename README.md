# Instance Manager Group Helm Chart

## Configuration

Ensure the `KUBECONFIG` environment variable is pointing to a valid Kubernetes configuration file.

If you don't have a cluster available, one can be created using [this](https://github.com/dhis2-sre/im-cluster) project.

## Deploy

```bash
skaffold run
```

## Helm

[Instance Manager Group helm chart](./charts/im-group) is published to https://dhis2-sre.github.io/im-group

To install the chart you first need to add this chart repository

```sh
helm repo add im-group https://dhis2-sre.github.io/im-group
helm repo update
helm search repo im-group/im-group --versions
```

The versions returned are gathered from [index.yaml](./index.yaml) which is published
to [this GitHub page](https://dhis2-sre.github.io/im-group/index.yaml).

### Release

Bump the version in [Chart.yaml](./charts/im-group/Chart.yaml), commit and push.
**NOTE: do not create a tag yourself!**

Our release workflow will then using [Helm chart releaser action](https://github.com/helm/chart-releaser-action)

* create a tag `im-group-<version>`
* create a [release](https://github.com/dhis2-sre/im-group/releases) associated with the new tag
* commit an updated index.yaml with the new release
* redeploy the GitHub pages to serve the new index.yaml

Note: there might be a slight delay between the release and the `index.yaml` file being updated as GitHub pages have to
be re-deployed.
