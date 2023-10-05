<h1>ITTalent - Curso de DevOps 2023.2</h1>

Repositório do Hackathon - IT TALENT 2023.2

**Dupla:**

- Gabriel Lopes
- Gabriel Lins

---

- [A aplicação](#a-aplicação)
- [O Banco de Dados](#o-banco-de-dados)

---

## A aplicação

É uma simples API RESTful em Golang, com um CRUD básico de usuário.

## O Banco de Dados

Um banco de dados simples que utiliza o SGBD não-relacional MongoDB.

A estrutura do documento principal `user` é:

```json
{
  "user": 
  {
    "id": "ObjectID(\"<object_id_do_usuario>\")",
    "name": "Nome do usuário",
    "email": "email@dousuario.com",
    "password": "Senha do usuario"
  }
}
```

## Comandos Vagrant

### `Vagrant init`
Este comando é usado para inicializar um novo Vagrantfile no diretório atual. Ele cria um arquivo de configuração padrão que define as propriedades da máquina virtual.

### `Vagrant up`
Este comando é usado para criar e configurar a máquina virtual com base no Vagrantfile presente no diretório. Se a máquina já estiver criada, ele irá iniciá-la.

### `Vagrant ssh cliente`
Este comando é usado para acessar a máquina virtual do cliente via SSH. 

#### Provisionamento do Cliente
O Vagrantfile do cliente contém os seguintes comandos de provisionamento:

```bash
apt-get update                  # Atualiza a lista de pacotes
apt-get upgrade -y              # Atualiza os pacotes instalados
apt-get install -y curl vim htop # Instala os pacotes curl, vim e htop
```

### `Vagrant ssh servidor`
Este comando é usado para acessar a máquina virtual do servidor via SSH.

#### Provisionamento do Servidor
O Vagrantfile do servidor contém os seguintes comandos de provisionamento:

```bash
sudo yum -y update              # Atualiza todos os pacotes
sudo yum install -y yum-utils git wget  # Instala os pacotes yum-utils, git e wget
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo  # Adiciona o repositório do Docker
sudo yum install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin  # Instala o Docker e suas dependências
sudo systemctl start docker     # Inicia o serviço do Docker
sudo chmod 666 /var/run/docker.sock  # Altera as permissões do socket do Docker
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose  # Baixa o Docker Compose
sudo chmod +x /usr/local/bin/docker-compose  # Torna o Docker Compose executável
```

---
