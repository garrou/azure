# azure

The purpose of the project, create a virtual machine on azure with ubuntu 22.04. Then, with ansible, install docker, docker-compose and launch the docker-compose on the virtual machine. The purpose of the docker-compose.yml is to collect virtual machine logs with Promtail and display then with Loki and Grafana.

## Install Azure CLI to use Terraform locally

I use Terraform locally cause I can't access to the Active Directory of my organization to create a ClientID, ClientSecret and TenantID. But initialy, the purpose is create the virtual machine from Gitlab in a pipeline.

[Azure CLI](https://learn.microsoft.com/fr-fr/cli/azure/install-azure-cli-windows?tabs=azure-cli)

This allow us to connect to Azure

## Install Terraform locally

[Terraform](https://developer.hashicorp.com/terraform/downloads?product_intent=terraform)

## Check Azure locations with Azure CLI

```sh
az account list-locations
```

## Check Azure available image with Azure CLI

```sh
az vm image list
```

## Launch Terraform

```sh
.\terraform\terraform.exe -chdir="./terraform" init
.\terraform\terraform.exe -chdir="./terraform" plan
.\terraform\terraform.exe -chdir="./terraform" apply
```

## Connect to VM with SSH to check if VM is OK

```sh
ssh -i <private key path> <user>@<public-ip>
```

## Launch Ansible playbook 

### Locally 

```sh
ansible-playbook -i ansible/inventory ansible/playbook-docker.yml -u <user> --private-key=~/.ssh/id_rsa
```

### Gitlab

Ansible run in .gitlab-ci.yml

### Check Grafana

```sh
<public-ip>:3000
```