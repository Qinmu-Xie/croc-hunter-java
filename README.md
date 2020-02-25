# Croc Hunter - The game!  funny

For those that have dreamt to hunt crocs

# Usage

Basic [Quarkus](https://quarkus.io/) app to demonstrate example CI/CD pipeline using Kubernetes

# Local Development

Quarkus comes with a [built-in development mode](https://quarkus.io/guides/maven-tooling). Run your application with:

```bash
mvn compile quarkus:dev
```

`mvn package` will build a native image.


# Deploy using JenkinsX (Kubernetes, Helm, Monocular, ChartMuseum)

Just follow the [JenkinsX](http://jenkins-x.io) installation with Tekton

For example, if using GKE

```bash
jx install \
    --provider=gke \
    --tekton
jx upgrade ingress
```

Then fork this repo and [import it](http://jenkins-x.io/developing/import/)

```bash
jx import \
    --url https://github.com/GITHUB_USER/croc-hunter-java \
    --no-draft \
    --pack=maven
```

Then, any PRs against this repo will be automatically deployed to preview environments.
When they are merged they will be deployed to the `staging` environment.

To tail all the build logs

    kail -l tekton.dev/pipeline --since=5m

Or in [GKE StackDriver logs](https://console.cloud.google.com/logs/viewer)

```
resource.labels.cluster_name="mycluster"
resource.type="container"
labels."container.googleapis.com/namespace_name"="jx"
resource.labels.container_name:build-step-
```

To [promote from staging to production](http://jenkins-x.io/developing/promote/) just run

    jx promote croc-hunter-java --version 0.0.1 --env production

# Acknowledgements

Original work by [Lachlan Evenson](https://github.com/lachie83/croc-hunter)
Continuation of the awesome work by everett-toews.
* https://gist.github.com/everett-toews/ed56adcfd525ce65b178d2e5a5eb06aa

## Watch Their Demo

https://www.youtube.com/watch?v=eMOzF_xAm7w

