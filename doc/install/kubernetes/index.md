# Installing GitLab on Kubernetes
> **Note**: These charts have been tested on Google Container Engine and Azure Container Service. Other Kubernetes installations may work as well, if not please [open an issue](https://gitlab.com/charts/charts.gitlab.io/issues).

The easiest method to deploy GitLab on [Kubernetes](https://kubernetes.io/) is
to take advantage of GitLab's Helm charts. [Helm] is a package
management tool for Kubernetes, allowing apps to be easily managed via their
Charts. A [Chart] is a detailed description of the application including how it
should be deployed, upgraded, and configured.

## Chart Overview

* **[GitLab-Omnibus](#gitlab-omnibus-chart-recommended)**: The best way to run GitLab on Kubernetes today. It is suited for small to medium deployments, and is in beta while support for backups and other features are added.
* **[Upcoming Cloud Native Charts](#upcoming-cloud-native-helm-charts)**: The next generation of charts, currently in development. Will support large deployments, with horizontal scaling of individual GitLab components.
* Other Charts
  * [GitLab Runner Chart](#gitlab-runner-chart): For deploying just the GitLab Runner.
  * [Advanced GitLab Installation](#advanced-gitlab-installation): Provides additional deployment options, but provides less functionality out-of-the-box. It's beta, no longer actively developed, and will be deprecated by [gitlab-omnibus](#gitlab-omnibus-chart-recommended) once it supports these options.
  * [Community Contributed Charts](#community-contributed-charts): Community contributed charts, deprecated by the official GitLab charts.

## GitLab-Omnibus Chart (Recommended)
> **Note**: This chart is in beta while [additional features](https://gitlab.com/charts/charts.gitlab.io/issues/68) are being added.

This chart is the best available way to operate GitLab on Kubernetes. It deploys and configures nearly all features of GitLab, including: a [Runner](https://docs.gitlab.com/runner/), [Container Registry](../../user/project/container_registry.html#gitlab-container-registry), [Mattermost](https://docs.gitlab.com/omnibus/gitlab-mattermost/), [automatic SSL](https://github.com/kubernetes/charts/tree/master/stable/kube-lego), and a [load balancer](https://github.com/kubernetes/ingress/tree/master/controllers/nginx). It is based on our [GitLab Omnibus Docker Images](https://docs.gitlab.com/omnibus/docker/README.html).

Once the [cloud native charts](#upcoming-cloud-native-helm-charts) are ready for production use, this chart will be deprecated. Due to the difficulty in supporting upgrades to the new architecture, migrating will require exporting data out of this instance and importing it into the new deployment.

Learn more about the [gitlab-omnibus chart.](gitlab_omnibus.md)

## Upcoming Cloud Native Charts

GitLab is working towards building a [cloud native deployment method](https://gitlab.com/charts/helm.gitlab.io/blob/master/README.md). A key part of this effort is to isolate each service into its [own Docker container and Helm chart](https://gitlab.com/gitlab-org/omnibus-gitlab/issues/2420), rather than utilizing the all-in-one container image of the [current charts](#official-gitlab-helm-charts-recommended).

By offering individual containers and charts, we will be able to provide a number of benefits:
* Easier horizontal scaling of each service,
* Smaller, more efficient images,
* Potential for rolling updates and canaries within a service,
* and plenty more.

This is a large project and will be worked on over the span of multiple releases. For the most up-to-date status and release information, please see our [tracking issue](https://gitlab.com/gitlab-org/omnibus-gitlab/issues/2420). We do not expect these to be production ready before the second half of 2018.

## Other Charts

### GitLab Runner Chart

If you already have a GitLab instance running, inside or outside of Kubernetes, and you'd like to leverage the Runner's [Kubernetes capabilities](https://docs.gitlab.com/runner/executors/kubernetes.html), it can be deployed with the GitLab Runner chart.

Learn more about [gitlab-runner chart.](gitlab_runner_chart.md)

### Advanced GitLab Installation

If advanced configuration of GitLab is required, the beta [gitlab](gitlab_chart.md) chart can be used which deploys the core GitLab service along with optional Postgres and Redis. It offers extensive configuration, but offers limited functionality out-of-the-box; it's lacking Pages support, the container registry, and Mattermost. It requires deep knowledge of Kubernetes and Helm to use.

This chart will be deprecated and replaced by the [gitlab-omnibus](gitlab_omnibus.md) chart, once it supports [additional configuration options](https://gitlab.com/charts/charts.gitlab.io/issues/68). It's beta quality, and since it is not actively under development, it will never be GA.

Learn more about the [gitlab chart.](gitlab_chart.md)

### Community Contributed Charts

The community has also [contributed GitLab charts](https://github.com/kubernetes/charts/tree/master/stable/gitlab-ce) to the [Helm Stable Repository](https://github.com/kubernetes/charts#repository-structure). These charts should be considered [deprecated](https://github.com/kubernetes/charts/issues/1138) in favor of the [official Charts](#official-gitlab-helm-charts-recommended).

[chart]: https://github.com/kubernetes/charts
[helm]: https://github.com/kubernetes/helm/blob/master/README.md
