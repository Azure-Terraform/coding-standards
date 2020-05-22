# Best Practice for Terraform Module Creation
The aim of this document is to provide a best-practice framework for creating Terraform Modules.
This will help ensure all terraform modules follow a consistent format and structure.

#### Repository Structure
* README.md - Documentation and example usage
* versions.tf - Provider version locking
* variables.tf - Input variables
* output.tf
* main.tf

#### Module Usage
When consuming a Terraform module the source should always be versioned.
Where possible all code should be locked to a version to prevent issues in future.
A conscious effort should be made to bring these versions up-to date on a regular basis.

#### Resource Tagging
If a resource accepts tag values these must be used.
Please reference the tagging policy for the relevant cloud to ensure you are compliant.

#### Comments and Readability
All comments should use a single hash, space followed by the comment
Example Usage:<br />
> \# Example comment<br />

If count is specified it should always be the first variable.
Tags should be the last variable to ensure code is readable.

Example Usage:<br />
> resource "example_resource" "example_name" {<br />
>&nbsp;&nbsp;count = x<br />
>&nbsp;&nbsp;<br />
>&nbsp;&nbsp;name = "example-resource"<br />
>&nbsp;&nbsp;....<br />
>&nbsp;&nbsp;tags = ['example']<br />
>}<br />

#### Input Variables
All input variables must have description and type.
The structure for inputs is:
 - Description
 - Type
 - Default (if defined)

Example Usage:<br />
>variable "example_input_variable" {<br />
>&nbsp;&nbsp;description = "This is an example input variable"<br />
>&nbsp;&nbsp;type&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;= string<br />
>&nbsp;&nbsp;default&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;= "example"<br />
>}<br />

#### Providers
Terraform providers should not be specified within a module.
Instead use the required_provider option, all providers should also include a minimum version.

Example Usage:<br />
>terraform {<br />
>&nbsp;&nbsp;required_version = ">= 0.12.20"<br />
>&nbsp;<br />
>&nbsp;&nbsp;required_providers {<br />
>&nbsp;&nbsp;&nbsp;&nbsp;azurerm = ">= 2.0.0"<br />
>&nbsp;&nbsp;}<br />
>&nbsp;<br />
>}<br />
