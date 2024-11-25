
# Configuração do Ambiente com Vagrant e Docker

Este guia detalha como configurar um ambiente de desenvolvimento para aplicações Laravel e React utilizando **Vagrant** e **Docker**.

---

## Pré-requisitos

Certifique-se de ter os seguintes softwares instalados:

- **Vagrant** ([Guia de instalação](https://www.vagrantup.com/docs/installation)).
- **VirtualBox** ou outro provedor compatível com Vagrant.
- **Docker** e **Docker Compose** instalados na máquina host.

---

## Configuração do Vagrant

### Vagrantfile

O `Vagrantfile` configura uma máquina virtual com Ubuntu Server, Docker e Docker Compose instalados. As portas dos serviços são mapeadas para a máquina host:

| Serviço        | Porta Host | Porta Guest |
|----------------|------------|-------------|
| Nginx          | 8080       | 80          |
| MySQL          | 3306       | 3306        |
| PhpMyAdmin     | 8891       | 80          |
| Redis          | 6379       | 6379        |
| MailHog (SMTP) | 1025       | 1025        |
| MailHog (Web)  | 8025       | 8025        |
| React          | 5173       | 5173        |
| Laravel        | 8000       | 8000        |

---

## Inicialização do Ambiente

1. Na raiz do projeto, execute:
   ```bash
   vagrant up
   ```

2. Acesse a VM:
   ```bash
   vagrant ssh
   ```

3. Certifique-se de estar na pasta sincronizada:
   ```bash
   cd /home/vagrant/drive
   ```

---

## Clonando os Repositórios

Clone os repositórios dentro da pasta sincronizada na VM:
```bash
git clone https://github.com/HACKATON-4-SEMESTRE-UNIALFA/API.git
git clone https://github.com/HACKATON-4-SEMESTRE-UNIALFA/Page.git
```

---

## Subindo os Containers

1. Acesse a pasta do projeto Laravel (`API`):
   ```bash
   cd API
   ```

2. Suba os containers com:
   ```bash
   docker-compose up -d
   ```

Se as dependências não forem instaladas automaticamente:
- Para Laravel:
  ```bash
  composer install
  ```
- Para React:
  ```bash
  cd ../Page
  npm install
  ```

---

## Iniciando o React

Caso o React não inicie automaticamente:
```bash
docker-compose up -d react
```

---

## Verificação do Status dos Containers

Certifique-se de que todos os containers estão rodando:
```bash
docker ps
```

---

## Configurações de Acesso

- **PhpMyAdmin**: Acesse em [http://localhost:8891](http://localhost:8891).
- **React**: Acesse em [http://localhost:5173](http://localhost:5173).
- **Laravel**: Acesse em [http://localhost:8000](http://localhost:8000).

---

## Executando Migrations

Se as migrations não forem executadas automaticamente, rode:
```bash
docker-compose run --rm artisan migrate
```

---

## Solução de Problemas

- Certifique-se de que a pasta sincronizada foi configurada corretamente no `Vagrantfile`.
- Verifique se o Docker está funcionando dentro da VM:
  ```bash
  docker --version
  docker-compose --version
  ```

- Caso ocorra erro de permissão no Docker, reconfigure os grupos de usuário:
  ```bash
  sudo usermod -aG docker vagrant
  ```

---

Este ambiente fornece uma configuração completa e pronta para o desenvolvimento com Laravel e React, integrando todos os serviços necessários para a aplicação.
