# 🅿️ EasyPark – DevOps

---

## Sobre o Projeto

O **EasyPark** é uma solução de **estacionamento inteligente com IoT**, desenvolvida para otimizar a ocupação de vagas e melhorar a experiência dos motoristas em estacionamentos.  
O sistema realiza o monitoramento de vagas em tempo real através de **sensores IoT** e disponibiliza as informações por meio de uma **API Java Spring Boot** hospedada na **nuvem Azure**.

O projeto foi implementado utilizando práticas modernas de **DevOps e Cloud Computing**, incluindo:
- Provisionamento automatizado de infraestrutura com **Azure CLI**;  
- Containerização da aplicação via **Docker**;  
- Orquestração com **Docker Compose**;  
- Deploy em **máquina virtual Linux** na Azure;  
- Monitoramento de desempenho e alertas de CPU.

---

## Estrutura do Diretório

```
DevOps/
├── evidencias/                    # Evidências e screenshots do processo de deploy
├── README.md                      # Documentação principal do projeto
├── setup-azure.md                 # Comandos para criar e configurar a VM no Azure
└── setup-docker.md                # Instalação do Docker e deploy da aplicação
```

---

## Arquitetura na Nuvem Azure

A aplicação é executada em uma **Azure Virtual Machine** com os seguintes parâmetros:

| Recurso | Valor |
|----------|--------|
| Resource Group | `EasyPark` |
| Nome da VM | `VMEasyPark` |
| Localização | `Canada Central` |
| Tamanho | `Standard_B2s (2 vCPUs, 4GB RAM)` |
| Sistema Operacional | Ubuntu 24.04 |
| Porta Aplicação | 8080 |
| Admin User | `admlnx` |

**Monitoramento:**  
Um alerta foi configurado para notificar quando o uso de CPU ultrapassar **90%** por **5 minutos consecutivos**, garantindo a estabilidade da aplicação.

---

## Docker e Containerização

Os arquivos de containerização estão localizados no diretório da aplicação Java:

- **Dockerfile** → `easypark/Dockerfile`
- **Docker Compose** → `easypark/compose.yaml`

### Estratégia de Build Multi-stage

1. **Build Stage**  
   - Base: `eclipse-temurin:21-jdk`  
   - Compila a aplicação com Maven (`mvn clean package -DskipTests`)

2. **Runtime Stage**  
   - Base: `eclipse-temurin:21-jre`  
   - Copia apenas o `.jar` final e executa com `java -jar app.jar`  
   - Usuário não-root para maior segurança  

### Docker Compose

```yaml
services:
  easypark-api:
    build:
      context: .
    env_file:
      - .env
    container_name: easypark-api
    restart: unless-stopped
    ports:
      - "8080:8080"
```

---

## Deploy Passo a Passo

### 1. Criar e Preparar a VM no Azure

```bash
# Criação do grupo de recurso
az group create --name "EasyPark" --location "canadacentral"

# Criação da máquina virtual
az vm create   --resource-group "EasyPark"   --name "VMEasyPark"   --image "Ubuntu2404"   --size "Standard_B2s"   --authentication-type "password"   --admin-username "admlnx"   --admin-password "Fiap@2tdspsvm"
```

### 2. Abrir Portas e Configurar Alerta

```bash
az vm open-port --resource-group "EasyPark" --name "VMEasyPark" --port 8080 --priority 1001

az monitor metrics alert create   --name "Alert-CPU-High"   --resource-group "EasyPark"   --scopes $(az vm show -g EasyPark -n VMEasyPark --query id -o tsv)   --description "CPU acima de 90% por 5 minutos"   --condition "avg Percentage CPU > 90"
```

### 3. Conectar à VM

```bash
ssh admlnx@<IP_PUBLICO_DA_VM>
```

### 4. Instalar Docker e Docker Compose

```bash
sudo apt-get update -y
sudo apt-get install docker.io -y
sudo apt-get install docker-compose -y
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker ${USER}
exit
```

Após reconectar à VM:

```bash
docker ps
docker-compose --version
```

### 5. Clonar o Repositório e Subir o Container

```bash
git clone https://github.com/kgb-fiap/easypark-java.git
cd easypark

echo -e "DB_USER=user\nDB_PASSWORD=pass" > .env
docker-compose up -d
```

### 6. Testar a Aplicação

```bash
curl http://localhost:8080/vagas
# ou via IP público
curl http://<IP_PUBLICO>:8080/vagas
```

---

🔗 **Repositório GitHub:** [https://github.com/kgb-fiap/easypark-devops.git](https://github.com/kgb-fiap/easypark-devops.git)  
🎥 **Vídeo de Demonstração:** [https://youtu.be/oMKW7f8RNwg](https://youtu.be/oMKW7f8RNwg)