# notes related to ci/cd pipeline

## basics

- build artifacts
  - containerized apps or app services
  - packages with app binaries (structured zip file)

- container registry
  - is used to store containers and deploy them into different environments

- iac: infrastructure as code
- gitops: applying iac best practice of having git repo as a single source of truth 
  - push model: using pull request and going through ci/cd pipeline to propagate changes
  - pull model: monitoring some branches and propagating changes automatically as soon as they appear


## gitlab

- key entities
  - configuration file
    - used by GitLab Runner to manage your project’s jobs and stored in a YAML format
    - filename: .gitlab-ci.yml

  - runner: is an application (build agent) that works with GitLab CI/CD to run jobs in a pipeline

  - jobs: are set of commands that stored in section script in a config file. GitLab Runner runs jobs in a host machine

  - stage
    - allows to group jobs, and jobs of the same stage are executed in parallel
    - jobs of the next stage are run after the jobs from the previous stage complete successfully

  - pipeline: is a group of jobs that get executed in stages (batches)

  - artifact: is a list of files and directories which are attached to a job after it completes successfully
  - environments: are like tags for your CI jobs, describing where code gets deployed

  - executors
    - GitLab Runner implements a number of executors that can be used to run your builds in different environments
    - examples: ssh, shell, docker, kubernetes, etc.

  - kubernetes executor [1]
    - calls the Kubernetes cluster API and creates a pod for each GitLab CI job
        - creates the Pod against the Kubernetes Cluster. This creates the containers required for the build and services to run
        - clones, restores cache, and downloads artifacts from previous stages. This step runs on a special container as part of the pod
        - runs user build
        - creates cache, uploads artifacts to GitLab. This step also uses the special container as part of the pod

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
  - yaml is used to define pipelines
    - it was not designed to be a programming language
    - may quickly become hard to understand
  - you can't declare multiple pipeline-templates within one repository
    - there is an ugly way with setting a variable triggering set of jobs
  - a bit confusing terminology (not a big deal)
    - pipeline instance is called 'pipeline' and pipeline is called 'pipeline template'
  - does not support prepopulation of values for parametrized pipelines (but jenkins does if i remember correctly)


## jenkins

- industry standard tool for ci/cd
- rich ecosystem of plugins
- groovy dsl for defining pipelines
- cons
  - plugins are not always up to date or well supported
  - a bit archaic and glitchy interface (as of 2019)
  - lack of analytics for overall tracking of pipelines [^2]


## azure devops (azdo)

- tutorials
  - azure devops tutorial for beginners | ci/cd with azure pipelines https://www.youtube.com/watch?v=4BibQ69MD8c


### pipelines

- key entities
  - stages usually contain set of jobs
  - jobs usually contain set of steps
    - can depend on other jobs
  - task
    - a packaged reusable piece of functionality 
    - there are standard tasks as well as custom added ones
    - tasks can be 'masked' as keywords
      - e.g. 'publish' keyword is a shortcut for the 'publish pipeline artifact' task

- you can specify custom name for a pipeline as of september 13, 2022
  - which means you can declare multiple pipelines within the same repository

- to make stages run in parallel
  - add empty dependsOn: attribute to stage https://stackoverflow.com/questions/67912631/devops-cicd-parallel-stages-deployment
  
- disadvantages
  - ms architects making same old mistakes over and over again
    - pipelines need a rich DSL in order to be able to harness complexity of ci/cd
    - yaml-based programming languages are recipe for a failure (remember cold fusion?)
    - any attempts to do programming in yaml end up in tons of shitty code
    - or maybe this is done in order to discourage people to create complicated pipelines?
      - if this is the case - its not working as intended ;)

  - pipeline configuration interface is barebones and not intuitive in comparison with competitors

  - poor terminology: jobs, steps, tasks
    - you can't guess what is what without reading documentation
  - release pipelines are not declarative, but defined using clunky gui
  - pipeline cancellation is implemented poorly (for users), so when you cancel pipeline it still trying to finish started job, no matter how long it takes
    - so if you pay for azdo pipelines from your wallet, it will likely get pretty expensive for no good reason
  - cache is not local to runners, so it may take quite a while to just download it to the runner
    - this defies the very purpose of caching for some class of tasks (like pip installing things, as it just downloads things as well)
  - selecting specific stages while manually triggering pipeline does not respect dependsOn attribute
    - this is happens when you set dependsOn attribute in 'stage', so that it depends on some other stage
    - it just skips stage runs for dependencies and likely will fail
  - jobs within same stage can be executed in-parallel but there is no graph visualization for them
  - live logs screen sometimes missing messages, unless you reload a page


### azure artifacts

- 'azure artifacts' is the name of the product
- belongs to 'aftifacts repository' class of products
- supports following package types: nuget, npm, maven, python, universal packages
- key entities
  - feed
    - associated with
      - a project within an organization
    - has a visibility level
      - public: available to everyone
      - private
        - scoped to project
        - inherits visibility policies from its project

- problems
  - product documentation 
    - pretty confusing definition of what 'feed' is
      - url: https://docs.microsoft.com/en-us/azure/devops/artifacts/concepts/feeds?view=azure-devops
      - terminology is confusing
      - 'artifacts feed' concept is used instead of 'aftifacts repository'
      - 'public registries' concept is used when referring to a third-party artifacts repositories
    - legacy, historical aspects of how product was evolving are mangled with things that really matter in some doc pages



## reference

[^1]: https://docs.gitlab.com/ee/operations/feature_flags.html#choose-a-client-library
[^2]: https://www.lambdatest.com/blog/jenkins-vs-gitlab-ci-battle-of-ci-cd-tools/
