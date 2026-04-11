# 🅿️ EasyPark – DevOps

---

## Sobre o Projeto

O **EasyPark** é uma solução de **estacionamento inteligente com IoT**, desenvolvida para otimizar a ocupação de vagas e melhorar a experiência dos motoristas em estacionamentos.  
O sistema realiza o monitoramento de vagas em tempo real através de **sensores IoT** e disponibiliza as informações por meio de uma **API Java Spring Boot** hospedada na **nuvem Azure**.
Aqui está **tudo em um README.md único**, organizado, limpo e pronto pra copiar e colar direto no GitHub:

---

````markdown
# 🚗 EasyPark - API de Vagas

Projeto de API para controle de vagas usando Spring Boot, Oracle e Azure com CI/CD.

---

## 1. Baixar o projeto (EasyPark)

- Acesse o repositório  
- Baixe ou clone:

```bash
git clone https://github.com/Vi-debu/easypark-java.git
````

* Abra no IntelliJ ou VS Code

---

## 2. Configurar conexão com o banco

Arquivo:

```
src/main/resources/application.properties
```

Altere:

* URL do banco Oracle
* Usuário
* Senha

---

## 3. Subir o projeto no GitHub

```bash
git add .
git commit -m "subindo projeto"
git push
```

---

## 4. Criar o Web App na Azure

* Acesse o portal da Azure
* Crie um **App Service (Web App)**

Configure:

* Nome da aplicação
* Região
* Runtime Java

---

## 5. Conectar com GitHub (CI/CD)

* Habilite implantação contínua
* Autorize sua conta do GitHub
* Selecione:

  * Repositório: easypark-java
  * Branch: main

---

## 6. Deixar o pipeline rodar

* Vá no GitHub → **Actions**
* Verifique:

  * Build rodando
  * Deploy rodando

---

## 7. Testar a API

URL base:

```
https://api-easypark-agh6f3dugbemcfbh.canadacentral-01.azurewebsites.net
```

Endpoint:

```
/vagas
```

Exemplo:

```
https://api-easypark-agh6f3dugbemcfbh.canadacentral-01.azurewebsites.net/vagas
```

---

## 8. Testar no Postman

### GET → listar vagas

```json
{
  "content": [
    {
      "id": 1823,
      "codigo": "B20-3ANDAR",
      "ativa": false,
      "nivelId": 341,
      "tipoVagaId": 122
    },
    {
      "id": 1661,
      "codigo": "V00-01",
      "ativa": true,
      "nivelId": 341,
      "tipoVagaId": 122
    }
  ]
}
```

---

### POST → criar vaga

```json
{
  "nivelId": 341,
  "tipoVagaId": 122,
  "codigo": "VAGA-TESTE-01",
  "ativa": true
}
```

---

### PUT → atualizar vaga

```json
{
  "nivelId": 341,
  "tipoVagaId": 122,
  "codigo": "VAGA-TESTE-01-EDITADA",
  "ativa": false
}
```

---

### DELETE → apagar vaga

* Troque o método para **DELETE**
* Clique em **Send**

---

## 9. Conferir no banco

```sql
SELECT * FROM tb_vagas;
```

Verifique se os dados foram alterados.

---

## 10. Finalizar

* Delete os recursos da Azure

---


## **Criadores**

* [@gabrielCZz](https://github.com/orgs/kgb-fiap/people/gabrielCZz) - Gabriel Cruz | RM 559613
* [@k-auaferreira](https://github.com/orgs/kgb-fiap/people/k-auaferreira) - Kauã Ferreira | RM 560992
* [@Vi-debu](https://github.com/orgs/kgb-fiap/people/Vi-debu) - Vinicius Bitú | RM 560227

---

🔗 **Repositório GitHub:** [https://github.com/kgb-fiap/easypark-devops.git](https://github.com/kgb-fiap/easypark-devops.git)  
🎥 **Vídeo de Demonstração:** [(https://youtu.be/pxm7_kMZyfE](https://youtu.be/pxm7_kMZyfE)
