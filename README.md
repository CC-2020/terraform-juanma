# terraform-juanma

Instala Terraform en la máquina anterior

        wget https://releases.hashicorp.com/terraform/0.12.24/terraform_0.12.24_linux_amd64.zip
        sudo apt install unzip
        unzip terraform_0.12.24_linux_amd64.zip
        sudo mv terraform /usr/local/bin

        terraform –version

Crear los ficheros necesarios con Terraform para crear una infraestructura a tu elección en GCP

        Hemos usado el proyecto cloud-shield de:
        https://github.com/terraform-providers/terraform-provider-google.git

        Para instalarlo
        git clone https://github.com/terraform-providers/terraform-provider-google.git
        cd terraform-provider-google/examples/
        cd cloud-armor/

        Tenemos que especificar un proveedor y credenciales
        nano "~/.gcloud/Terraform.json"

        provider "google" {
          credentials = file("account.json")
          project     = "my-project-id"
          region      = "us-central1"
        }

        Especificamos variables:
        nano variables.tf 

        variable "region" {
          default = "us-central1"
        }

        variable "region_zone" {
          default = "us-central1-a"
        }

        variable "project_name" {
          description = "infraestructura-como-codigo"
        }

        variable "credentials_file_path" {
          description = "Path to the JSON file used to describe your account credentials"
          default     = "~/.gcloud/Terraform.json"
        }

        variable "ip_white_list" {
          description = "A list of ip addresses that can be white listed through security policies"
          default     = ["192.0.2.0/24"]
        }

Ejecutamos el proyecto terraform:

        terraform init
        terraform plan -out=tfplan
        terraform apply
