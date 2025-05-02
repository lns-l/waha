# WAHA - WhatsApp HTTP API com Docker Compose

Este projeto utiliza [WAHA (WhatsApp HTTP API)](https://github.com/devlikeapro/wa-automate-host) com Docker Compose para facilitar a execução local com configuração via `.env`.

## 📆 Requisitos

* [Docker](https://www.docker.com/)
* [Docker Compose](https://docs.docker.com/compose/)

## 🚀 Como usar

### 1. Clone este repositório

```bash
git clone https://github.com/seu-usuario/waha-docker.git
cd waha-docker
```

### 2. Configure o arquivo `.env`

Edite o arquivo `.env` com as variáveis apropriadas.

### 3. Suba o container com Docker Compose

```bash
docker-compose up
```

A aplicação estará disponível em `http://localhost:3000`.

## 📁 Estrutura do projeto

```
.
├── docker-compose.yml
├── .env
└── README.md
```

## ⚙️ Exemplo de docker-compose.yml

```yaml
version: '3.8'

services:
  waha:
    image: devlikeapro/waha
    ports:
      - "3000:3000"
    volumes:
      - waha_data:/app/data
    environment:
      - WHATSAPP_API_PORT=3000
      - WHATSAPP_API_KEY=${WHATSAPP_API_KEY}
      - WAHA_LOG_LEVEL=${WAHA_LOG_LEVEL}
    stdin_open: true
    tty: true

volumes:
  waha_data:
```

## 📄 Exemplo de `.env`

```dotenv
# Configurações da API
WHATSAPP_API_PORT=3000
WHATSAPP_API_HOSTNAME=localhost
WHATSAPP_API_SCHEMA=http
WAHA_BASE_URL=http://localhost:3000

# Segurança da API
WHATSAPP_API_KEY=admin123

# Dashboard (WAHA Plus)
WAHA_DASHBOARD_ENABLED=true
WAHA_DASHBOARD_USERNAME=admin
WAHA_DASHBOARD_PASSWORD=admin

# Swagger
WHATSAPP_SWAGGER_ENABLED=true
WHATSAPP_SWAGGER_USERNAME=admin
WHATSAPP_SWAGGER_PASSWORD=admin
WHATSAPP_SWAGGER_TITLE=WAHA API
WHATSAPP_SWAGGER_DESCRIPTION=Documentação da API WAHA
WHATSAPP_SWAGGER_EXTERNAL_DOC_URL=https://waha.devlike.pro/docs/

# Logging
WAHA_LOG_FORMAT=PRETTY
WAHA_LOG_LEVEL=info
WAHA_HTTP_LOG_LEVEL=info

# Sessões
WAHA_AUTO_START_DELAY_SECONDS=5
WAHA_PRINT_QR=true
WAHA_WORKER_ID=waha1
WHATSAPP_RESTART_ALL_SESSIONS=true

# Webhooks globais
WHATSAPP_HOOK_URL=https://webhook.site/your-uuid
WHATSAPP_HOOK_EVENTS=message,message.any,state.change
WHATSAPP_HOOK_HMAC_KEY=your-secret-key
WHATSAPP_HOOK_RETRIES_POLICY=linear
WHATSAPP_HOOK_RETRIES_DELAY_SECONDS=2
WHATSAPP_HOOK_RETRIES_ATTEMPTS=4
WHATSAPP_HOOK_CUSTOM_HEADERS=X-Custom-Header:Value

# Armazenamento de arquivos
WHATSAPP_DOWNLOAD_MEDIA=true
WHATSAPP_FILES_FOLDER=/app/data
```

## 🔐 Acesso à API

Utilize o valor definido em `WHATSAPP_API_KEY` para autenticar:

```bash
curl -H "apikey: admin123" http://localhost:3000/status
```

## 📊 Acesso ao Dashboard

Se ativado, estará disponível em: `http://localhost:3000/dashboard`
Usuário/senha: definidos por `WAHA_DASHBOARD_USERNAME` e `WAHA_DASHBOARD_PASSWORD`.

## 📚 Swagger UI

Disponível em: `http://localhost:3000/docs` (caso ativado via `.env`)

## 🧰 Testes com Webhook

Use [Webhook.site](https://webhook.site) para receber e visualizar eventos.

## 📂 Persistência de Dados

Os dados são salvos no volume `waha_data`, montado em `/app/data`.

## 🪤 Finalizar

Para parar os containers:

```bash
docker-compose down
```

Para remover containers e volumes:

```bash
docker-compose down -v
```

---

📬 Dúvidas ou sugestões? Abra uma issue ou entre em contato com os mantenedores.
