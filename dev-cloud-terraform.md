# notes on terraform and related tools

- examples below assume that we defined 'tf' alias for 'terraform' command


## basics

- dependencies between resources
  - implicit: automatically configured based on resources referencing properties of other resources
  - explicit: use "depends_on" attribute

- marking resource for recreation
  - may happen when your cloud membership/plan imposes limitations on how existing resource can be modified
  - example
    > tf taint [module.<module-name>.]<resource-type>.<resource-id>

- destroy all provisioned resources
  > tf destroy

- see values for output variables
  > tf output

- save plan in human readable form into a file
  > tf plan -no-color > <filename>.txt


## custom scripts

- running custom scripts is possible by using external provider
  - as described in "Querying external data with Terraform" article [^1]

- such scripts can be any executable files
  - such files will be expected to take arguments in the form of json object and returning results in json form as well
  - results of the script will be accessible as properties of the function
    > data.external.<function-name>.result.<property-name>


## limitations

- there is no concept of 'self' when defining terraform resources, which sometimes leads to duplication in hcl code
- when it comes to loops and dynamic sections - design is pretty poor
  - tool hickups on simple features
  - documented functionality is not working giving misleading errors
    - example: try using var.my-var inside dynamic block or "iterator" property inside dynamic block and you will get nonsense errors


## useful tools

- automatic import of already existing resources in terraform
  - https://github.com/Azure/aztfexport (also referred as aztfy, terrafy)
  - https://github.com/magodo/tfadd
    - actually generates tf code based on state of the imported resource
  - https://github.com/cycloidio/terracognita
    - does not support eventhubs

  - tflint
    - warning: may not find some obvious mistakes that 'tf validate' finds


## alternatives

- terraform vs pulumi vs crossplane [^2]
  - crossplane
    - yaml definitions similar to k8s
      - this allows to store definitions together with other k8s resources
      - can leverage k8s ecosystem for managing/templating/modularizing/packaging definitions (helm, etc)
    - does not support previewing of a plan before applying changes
    - able to monitor infrastructural components in realtime and 'fix' differences immediately
    - needs k8s cluster to run
  - pulumi https://www.pulumi.com/
    - supports many programming languages for writing definitions
    - supports state tracking and plan command
  - terraform
    - industry standard for provisioning automation
    - clunky declarative syntax


## references

[^1]: https://subscription.packtpub.com/book/cloud-and-networking/9781800207554/2/ch02lvl1sec18/querying-external-data-with-terraform
[^2]: https://www.youtube.com/watch?v=RaoKcJGchKM