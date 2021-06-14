# **Treinamentos  Terraform**



![Terraform deployment workflow](./Imagens/terraform-iac.png)

Colocar ✔ quando concluído. 

## ✔ Descomplicando o Terraform | HashiWeek

- https://www.youtube.com/watch?v=8mRZJcCgoS0
- https://www.youtube.com/watch?v=lrAycU7_XnQ
- https://www.youtube.com/watch?v=4FellihAcV8



## ✔ Lucas de Souza - Terraform além do básico | #FiqueEmCasaConf

- https://www.youtube.com/watch?v=P3aY4_vxzWQ&t=243s

- https://github.com/souzaxx/terraform-alem-do-basico

  

## ✔ Como eu gostaria de ter aprendido - Terraform

https://www.youtube.com/watch?v=RLwvMDgVU80



## ✔ LinuxTips - HASHICORP EXPERT

- Descomplicando Terraform



## ✔ Oficial - Hashicorp

### Workshop

- https://hashiconf.com/europe/workshops/

### TUTORIALS

- https://learn.hashicorp.com/collections/terraform/modules?utm_source=WEBSITE&utm_medium=WEB_IO&utm_offer=ARTICLE_PAGE&utm_content=DOCS


- https://learn.hashicorp.com/terraform

  https://www.youtube.com/c/HashiCorp/search?query=terraform
- https://learn.hashicorp.com/collections/terraform/modules
- https://learn.hashicorp.com/collections/terraform/kubernetes
- https://learn.hashicorp.com/collections/terraform/aws

## Acloudguru
- Deploying to AWS with Terraform and Ansible

  

# **Anotações**

**Terraform é declarativo.** 



**terraform-cheatsheet**

https://res.cloudinary.com/acloud-guru/image/fetch/c_thumb,f_auto,q_auto/https://acg-wordpress-content-production.s3.us-west-2.amazonaws.com/app/uploads/2020/11/terraform-cheatsheet-from-ACG.pdf

**Hashicorp Configuration Language** (**HCL**)

### ## Voltar nesse cara - Modules

- https://www.terraform.io/docs/language/modules/index.html

![image-20210607202526718](./Imagens/image-20210607202526718.png)

### State

O terraform não funciona sem o arquivo de state. 

- https://www.terraform.io/docs/language/state/index.html

**Terraform Import**

Pega o que está no mundo real e coloca no state.

- https://www.terraform.io/docs/cli/import/index.html



### State Locking

- https://www.terraform.io/docs/language/state/locking.html

  

### Configuration Syntax

- https://www.terraform.io/docs/language/syntax/configuration.html
- https://github.com/hashicorp/hcl/blob/main/hclsyntax/spec.md

### Expressions

- https://www.terraform.io/docs/language/expressions/index.html
- https://www.terraform.io/docs/language/expressions/types.html

### Variables

- https://www.terraform.io/docs/language/values/variables.html

```yaml
The name of a variable can be any valid identifier except the following: source, version, providers, count, for_each, lifecycle, depends_on, locals.
```



**Backend**

**Backend com State Lock** - Toda vez que altera o backend tem que rodar o terraform init

**Remote State**

Mantem o estado do deploy.  Sempre quando vai atualizar ele verifica o local, verifica o remoto e aplica a diferença.

Dividir o state em lugares diferentes. 

**Dynamic Blocos**

Sempre utilizar 

**Workspaces**

Reutilizar o mesmo código para diversos ambientes.

Cria dentro do S3 (qdo state remoto) a pasta /env com cada workspaces.

![](./Imagens/image-20210601200725915.png)

- https://www.terraform.io/docs/language/state/workspaces.html




**Bloco Data** - coletar uma informação - recurso que já existe no Provider

```yaml
# ---------------------------------------------------------------------------------------------------------------------
data "aws_ami" "consul" {
  most_recent = true  ## Sempre a informação mais recente

  # If we change the AWS Account in which test are run, update this value.
  owners = var.owners ## Pegue a AMI cujo o dono seja "var.owners"

  filter {
    name   = "virtualization-type"
    values = ["hvm"]
  }

  filter {
    name   = "is-public"
    values = ["false"]
  }

  filter {
    name   = "name"
    values = ["consul-ubuntu-*"]
  }
}
```

Local name não é o nome da maquina, mas sim o nome de referencia no terraform

![image-20210531213602994](./Imagens/image-20210531213602994.png)

# **Comandos Terraform**

https://www.terraform.io/docs/cli/commands/index.html



|                         Comando                          | Descrição                                                    |
| :------------------------------------------------------: | :----------------------------------------------------------- |
|                    terraform **init**                    | Inicializa o ambiente com o provider utilizado.Por exemplo, se você estiver utilizando o **provider "aws"**, inicializa o plugin para Amazon Web Services. |
|                   terraform **apply**                    | Este comando que cria e altera as Instâncias/Objetos no Provider de acordo com o seu terraform. |
|                    terraform **plan**                    | Mostra o plano de execução do terraform.                     |
|                  terraform **destroy**                   | Este comando para as Instâncias/Objetos em execução e destruindo todos os recursos que foram criados durante o processo de criação. |
|                    terraform **show**                    | Mostra um resumo do status da sua infraestrutura terraform.  |
|                   terraform **output**                   | Mostra um valor de uma variável output                       |
|               terraform **init -upgrade**                | Upgrade de pacotes                                           |
|               terraform **plan -destroy**                | informa o plano de destruição                                |
|            terraform **apply -auto-approve**             | Cria infra automático sem perguntar                          |
|               terraform **workspace list**               | Lista os workspaces                                          |
|             terraform **workspace new dev**              | cria novos workspaces                                        |
|        terraform **workspace select "workspace"**        | altera o workspaces                                          |
|               terraform plan **-out out**                | Saída do arquivo plan, salva o plano em arquivo para ser executado exatamente como foi apresentado. |
|             terraform **state pull >> file**             | imprime o state file                                         |
|              terraform **state push file**               | altera o arquivo state, tem que aumentar o "serial", sempre incrementar |
|            terraform **destroy -lock=false**             | Ignora o lock // Serve para plan/apply                       |
| terraform **plan -lock=false -refresh=false -out plano** | Não faz refresh dos recursos // Serve para plan/appl         |
|                  terraform **refresh**                   | Atualiza o .state                                            |
|                   terrraform **state**                   | Altera o estado do state file                                |
|                  terraform **state rm**                  | Tirar o recurso da gerencia do Terraform                     |
|           terraform **-install-autocomplete**            | Instala o auto complete                                      |
|            **TF_LOG=DEBUG** terraform "tipo"             | Analise de logs                                              |
|                   terraform **taint**                    | Marcar um recurso que precisa ser destruído - SOMENTE NO PROXIMO PLAN e APPLY |
|                  terraform **untaint**                   | DesMarcar um recurso que precisa ser destruído               |
|                    terraform **fmt**                     | É usado para reescrever os arquivos de configuração do Terraform para um formato e estilo canônicos. |
|             terraform **init backend=false**             | Roda o init mas não sobe o backend                           |
|                                                          |                                                              |
|                                                          |                                                              |
|                                                          |                                                              |

# **Best Practices**



![image-20210531213708639](./Imagens/image-20210531213708639.png)
