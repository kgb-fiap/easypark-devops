# ☁️ Setup Azure - EasyPark 

Guia para criação de infraestrutura no Azure, incluindo **Resource Group**, **Virtual Machine**, abertura de portas e **alerta de monitoramento**.

---

## Criando o grupo de recurso

```bash
az group create --name "EasyPark" --location "canadacentral"
```

---

## Criando a máquina virtual

```bash
az vm create \
  --resource-group "EasyPark" \
  --name "VMEasyPark" \
  --image "Ubuntu2404" \
  --size "Standard_B2s" \
  --authentication-type "password" \
  --admin-username "admlnx" \
  --admin-password "Fiap@2tdspsvm" \
  --vnet-name "vnet-Linux" \
  --nsg "nsg-Linux" \
  --public-ip-address "pip-Linux" \
  --tags "owner=EasyPark"
```

---

## Abrindo portas 80 e 8080

```bash
az vm open-port --resource-group "EasyPark" --name "VMEasyPark" --port 80 --priority 1001
az vm open-port --resource-group "EasyPark" --name "VMEasyPark" --port 8080 --priority 1002
```

---

## Alerta para monitoramento de CPU

```bash
az monitor metrics alert create \
  --name "Alert-CPU-High" \
  --resource-group "EasyPark" \
  --scopes $(az vm show -g EasyPark -n VMEasyPark --query id -o tsv) \
  --description "CPU acima de 90% por 5 minutos" \
  --condition "avg Percentage CPU > 90"
```

---

## Deletando grupo de recursos

```bash
az group delete --name "EasyPark" --yes --no-wait
```