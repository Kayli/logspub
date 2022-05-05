# notes related to ci/cd pipeline

## basics

- build artifacts
  - containerized apps or app services
  - packages with app binaries (structured zip file)

- container registry
  - is used to store containers and deploy them into different environments


## gitlab

- features
  - git hosting
  - issue tracker
  - pipelines management
  - registries
    - container registry
    - terraform modules registry
    - packages with app binaries (structured zip file)
  - feature flags
    - integration with unleash [^1]
  - infrastructure as code with terraform
  - k8 provisioning using terraform
    - supports eks (elastic k8 service) or gke (google k8 engine)
  - container vulnerability scanning
  - good consistent documentation
  - integration with prometheus monitoring

- disadvantages
  - no ecosystem of plugins, so integrations are hardcoded


## jenkins

- industry standard tool for ci/cd
- rich ecosystem of plugins
- cons
  - plugins are not always up to date or well supported
  - a bit archaic and glitchy interface (as of 2019)
  - lack of analytics for overall tracking of pipelines [^2]


## reference

[^1]: https://docs.gitlab.com/ee/operations/feature_flags.html#choose-a-client-library
[^2]: https://www.lambdatest.com/blog/jenkins-vs-gitlab-ci-battle-of-ci-cd-tools/
