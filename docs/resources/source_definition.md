---
# generated by https://github.com/hashicorp/terraform-plugin-docs
page_title: "airbyte_source_definition Resource - terraform-provider-airbyte"
subcategory: ""
description: |-
  SourceDefinition resource
---

# airbyte_source_definition (Resource)

SourceDefinition resource

## Example Usage

```terraform
# Basic version of a custom source definition
resource "airbyte_source_definition" "basic" {
  name              = "basic_test"
  docker_repository = "eabrouwer3/airbyte-test-data-source"
  docker_image_tag  = "0.0.1"
  documentation_url = "https://github.com/eabrouwer3/airbyte-test-data-source"
}

# Much more complex version of a custom source definition
resource "airbyte_source_definition" "complex" {
  name              = "complex_test"
  docker_repository = "eabrouwer3/airbyte-test-data-source"
  docker_image_tag  = "0.0.1"
  documentation_url = "https://github.com/eabrouwer3/airbyte-test-data-source"

  default_resource_requirements = {
    cpu_request    = "0.25"
    cpu_limit      = "0.25"
    memory_request = "200Mi"
    memory_limit   = "200Mi"
  }

  job_specific_resource_requirements = [{
    job_type       = "sync"
    cpu_request    = "0.5"
    cpu_limit      = "0.5"
    memory_request = "500Mi"
    memory_limit   = "500Mi"
    }, {
    job_type       = "check_connection"
    memory_request = "50Mi"
    memory_limit   = "50Mi"
  }]
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `docker_image_tag` (String) Docker image tag
- `docker_repository` (String) Docker Repository URL (e.g. 112233445566.dkr.ecr.us-east-1.amazonaws.com/source-custom) or DockerHub identifier (e.g. airbyte/source-postgres)
- `documentation_url` (String) Documentation URL
- `name` (String) Source Definition Name

### Optional

- `default_resource_requirements` (Attributes) Actor definition specific resource requirements. If default is set, these are the requirements that should be set for ALL jobs run for this actor definition. It is overridden by the job type specific configurations. If not set, the platform will use defaults. These values will be overridden by configuration at the connection level. (see [below for nested schema](#nestedatt--default_resource_requirements))
- `job_specific_resource_requirements` (Attributes List) Sets resource requirements for a specific job type for an actor definition. These values override the default, if both are set. These values will be overridden by configuration at the connection level. (see [below for nested schema](#nestedatt--job_specific_resource_requirements))

### Read-Only

- `id` (String) Source Definition ID
- `protocol_version` (String) The Airbyte Protocol version supported by the connector
- `release_date` (String) The date when this connector was first released, in yyyy-mm-dd format
- `release_stage` (String) Allowed: alpha | beta | generally_available | custom

<a id="nestedatt--default_resource_requirements"></a>
### Nested Schema for `default_resource_requirements`

Optional:

- `cpu_limit` (String) CPU Limit
- `cpu_request` (String) CPU Requested
- `memory_limit` (String) Memory Limit
- `memory_request` (String) Memory Requested


<a id="nestedatt--job_specific_resource_requirements"></a>
### Nested Schema for `job_specific_resource_requirements`

Required:

- `job_type` (String) Allowed: get_spec | check_connection | discover_schema | sync | reset_connection | connection_updater | replicate

Optional:

- `cpu_limit` (String) CPU Limit
- `cpu_request` (String) CPU Requested
- `memory_limit` (String) Memory Limit
- `memory_request` (String) Memory Requested

