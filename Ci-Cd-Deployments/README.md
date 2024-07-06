
# Ci-Cd Deployments


- [Concourse _al](https://concourse-ci.org/docs.html): 
  - Concourse is a pipeline-based continuous thing-doer. 
  - Pipelines are built around Resources, which represent all external state, and Jobs, which interact with them. Concourse pipelines represent a dependency flow, kind of like distributed Makefiles. 
    - Resources like the git resource and s3 resource are used to express source code, dependencies, deployments, and any other external state. This interface is also used to model more abstract things like scheduled or interval triggers, via the time resource.
      - Resources make Concourse tick and are the source of automation within all Concourse pipelines. Resources are how Concourse interacts with the outside world. Here's a short list of some things that resources can do: You want something to run every five minutes? Time resource; You want to run tests on every new commit to the main branch? Git resource; Run unit tests on new PR's? Github-PR resource; Fetch or push the latest image of your app? Registry-image resource. Resources represent the external system or object to Concourse by emitting versions. When a new version is emitted by a resource, that is how Concourse knows to start trigger jobs.
    - Jobs are sequences of get, put, and task steps to execute. These steps determine the job's inputs and outputs. 
    - Makefile sets a set of rules to determine which parts of a program need to be recompile, and issues command to recompile them. They organize code compilation. Makefile is a way of automating software building procedure and other complex tasks with dependencies.
  - A Concourse installation is composed of a web node, a worker node, and a PostgreSQL node.
  - The first step to getting started with Concourse is to install the fly CLI tool. It has different commands.
  - Concourse configuration for things like Pipelines and Tasks is done through declarative YAML files. Concourse configuration supports basic variable substitution by way of ((vars)).
  - A pipeline is the result of configuring Jobs and Resources together. When you configure a pipeline, it takes on a life of its own, to continuously detect resource versions and automatically queue new builds for jobs as they have new available inputs. Pipelines are configured via fly set-pipeline or the set_pipeline step as declarative YAML files which conform to a schema. 
  - Each job has a single build plan configured as job.plan. A build plan is a recipe for what to run when a build of the job is created. A build plan is a sequence of steps: the task step runs a task, the get step fetches a resource, the put step updates a resource, the set_pipeline step configures a pipeline, the load_var step loads a value into a local var, the in_parallel step runs steps in parallel, the do step runs steps in sequence, the across step modifier runs a step multiple times; once for each combination of variable values, the try step attempts to run a step and succeeds even if the step fails, When a new version is available for a get step with trigger: true configured, a new build of the job will be created from the build plan.
  - [Concourse architecture _al](https://concourse-ci.org/internals.html)
- 


----------------------------------------------------------------------
