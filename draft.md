# Azion Terraform Provider 

[Terraform](https://developer.hashicorp.com/terraform/docs) is an infrastructure as code tool that makes it possible to manage your infrastructure efficiently through code. The files created to manage your infrastructure can be reused, versioned and shared, helping you to have a consistent workflow to provision and manage all of your infrastructure throughout its lifecycle. 

## How does Azion Terraform Provider work? 

Terraform works based [on providers](https://developer.hashicorp.com/terraform/registry/providers). A provider is responsible for managing the lifecycle of a particular resource type. Providers are implemented as plugins, being separate executable code that can be loaded into Terraform at Runtime.

[Azion Terraform Provider](https://github.com/aziontech/terraform-provider-azion) is an open source project, registered on [HashiCorp](https://www.hashicorp.com/). Working alongside [Azion SDK (Go)](https://github.com/aziontech/azionapi-go-sdk), it communicates with the Azion APIs as represented below:

![alt text for screen readers](./arch.png "Text to show on mouseover").

**Terraform Core** - You must have it installed on your environment, [Check how to install it here](https://developer.hashicorp.com/terraform/downloads). The Terraform core communicates to the Azion Terraform Provider. 

**Azion Terraform Provider** - Built in Go, it communicates with the Azion SDK (Go).

**Azion SDK (Go)** - Communicates with the Azion APIs.



In your Terraform files, you must set the Azion Terraform Provider as the provider and set its version as well, such as: 

```terraform
    required_providers {
        source = "aziontech/azion"
        version = "0.2.0" // it depends on the version you're willing to use.
    }
```

>**Note**: Currently **Azion Terraform Provider** is available only for managing you iDNS zones and records.

## Implementation

- [How to manage your iDNS zones with Azion Terraform Provider]()
- [How to manage your iDNS records with Azion Terraform Provider]()

## See also

- [iDNS]()
- [Azion Go SDK]()
- [Azion CLI]()