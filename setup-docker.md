# 🐳 Docker Setup — EasyPark

Guia para instalação, configuração e execução da aplicação **EasyPark** utilizando **Docker** e **Docker Compose**.

---

## Instalar o Docker

Atualize os pacotes e instale o Docker:

```bash
sudo apt-get update -y
sudo apt-get install docker.io -y
```

Ative e inicialize o serviço:

```bash
sudo systemctl start docker
sudo systemctl enable docker
```

Adicione o usuário atual ao grupo `docker`:

```bash
sudo usermod -aG docker ${USER}
```

> Após esse comando, é necessário **encerrar a sessão** para aplicar as permissões.

---

## Atualizar sessão

Saia da sessão atual:

```bash
exit
```

Após reconectar, teste se o Docker funciona sem `sudo`:

```bash
docker ps
```

---

## Instalar o Docker Compose

Instale o Docker Compose:

```bash
sudo apt-get install docker-compose -y
```

Verifique a instalação:

```bash
docker-compose --version
```

---

## Clonar o repositório do projeto

Clone o repositório da aplicação:

```bash
git clone https://github.com/kgb-fiap/easypark-java.git
```

Acesse a pasta da API Java:

```bash
cd easypark
```

---

## Definir variáveis de ambiente

Crie o arquivo `.env` com as credenciais do banco de dados:

```bash
echo -e "DB_USER=user\nDB_PASSWORD=pass" > .env
```

---

## Executar o Docker Compose

Suba os containers em segundo plano:

```bash
docker-compose up -d
```

Verifique se os containers estão ativos:

```bash
docker ps
```

Veja os logs de execução (substitua `<container_id>` pelo ID real):

```bash
docker logs <container_id>
```

---

## Testar a API

Teste o endpoint localmente:

```bash
curl http://localhost:8080/vagas && echo
```

Ou acesse via IP público da VM:

```bash
curl http://ippublico:8080/vagas
```

---

## Encerrar containers

Para parar e remover os containers criados pelo Compose:

```bash
docker-compose down
```