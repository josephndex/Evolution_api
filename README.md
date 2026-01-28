# Evolution API - WhatsApp Integration Stack

A complete Docker-based setup for Evolution API with PostgreSQL, Redis, and n8n integration for WhatsApp automation.

## 🚀 Services Overview

| Service | Description | Port | URL |
|---------|-------------|------|-----|
| **Evolution API** | WhatsApp API engine | 8080 | http://localhost:8080 |
| **Evolution Manager** | Built-in dashboard UI | 8080 | http://localhost:8080/manager/login |
| **PostgreSQL** | Database for persistence | 5432 | Internal |
| **Redis** | Cache and session management | 6379 | Internal |
| **n8n** | Workflow automation | 5678 | http://localhost:5678 |

## 📋 Prerequisites

- Docker & Docker Compose installed
- Minimum 4GB RAM available
- Ports 8080 and 5678 available

## 🛠️ Quick Start

### 1. Start All Services

```bash
docker-compose up -d
```

### 2. Check Service Status

```bash
docker-compose ps
```

### 3. View Logs

```bash
# All services
docker-compose logs -f

# Specific service
docker-compose logs -f evolution_api
```

## 🔐 Default Credentials

### Evolution API
- **API Key**: `B6D711FCDE4D4FD5936544120E713976`
- **Server URL**: `http://localhost:8080`

> ⚠️ **IMPORTANT**: Change the API key in production by modifying `AUTHENTICATION_API_KEY` in `docker-compose.yml`

### PostgreSQL Database
- **Database**: `evolution`
- **Username**: `evolution`
- **Password**: `evolution_pass`

## 📱 Accessing Evolution Manager

1. Open http://localhost:8080/manager/login
2. Enter credentials:
   - **Server URL**: `http://localhost:8080`
   - **API Key Global**: `B6D711FCDE4D4FD5936544120E713976`
3. Click **Login**

## 🔗 Connecting WhatsApp

1. Access Evolution Manager at http://localhost:8080/manager/login
2. Create a new instance
3. Scan the QR code with your WhatsApp mobile app
4. Your instance will be connected and ready

## 🔄 n8n Integration

Evolution API is pre-configured to work with n8n:

- **n8n Dashboard**: http://localhost:5678
- **N8N_ENABLED**: `true` (already enabled)

### Setting Up Webhooks in n8n

1. Create a new workflow in n8n
2. Add a Webhook trigger node
3. Configure Evolution API instance to send events to your n8n webhook URL
4. Build your automation workflow

## 📁 Data Persistence

Data is persisted using Docker volumes:

| Volume | Purpose |
|--------|---------|
| `evolution_instances` | WhatsApp session data |
| `postgres_data` | Database storage |
| `redis_data` | Cache data |

## 🛑 Managing Services

### Stop All Services
```bash
docker-compose down
```

### Stop and Remove Volumes (⚠️ Deletes all data)
```bash
docker-compose down -v
```

### Restart a Specific Service
```bash
docker-compose restart evolution_api
```

### Update Images
```bash
docker-compose pull
docker-compose up -d
```

## ⚙️ Configuration Options

### Webhook Events (Enabled by Default)

| Event | Description |
|-------|-------------|
| `MESSAGES_UPSERT` | New incoming/outgoing messages |
| `MESSAGES_UPDATE` | Message status updates |
| `MESSAGES_DELETE` | Deleted messages |
| `QRCODE_UPDATED` | QR code changes |
| `CONNECTION_UPDATE` | Connection status changes |
| `CONTACTS_UPSERT` | New contacts |
| `CHATS_UPDATE` | Chat updates |
| `GROUPS_UPDATE` | Group changes |
| `CALL` | Incoming calls |

### Available Integrations

| Integration | Status | Enable With |
|-------------|--------|-------------|
| n8n | ✅ Enabled | `N8N_ENABLED=true` |
| Typebot | ❌ Disabled | `TYPEBOT_ENABLED=true` |
| Chatwoot | ❌ Disabled | `CHATWOOT_ENABLED=true` |
| OpenAI | ❌ Disabled | `OPENAI_ENABLED=true` |
| Dify | ❌ Disabled | `DIFY_ENABLED=true` |

## 🐛 Troubleshooting

### Evolution API not starting
```bash
# Check logs
docker logs evolution_api

# Ensure PostgreSQL is healthy
docker logs evolution_postgres
```

### Cannot connect to WhatsApp
1. Delete the instance and create a new one
2. Make sure your phone has internet connection
3. Check if WhatsApp is up to date on your phone

### Reset Everything
```bash
docker-compose down -v
docker-compose up -d
```

## 📚 API Documentation

Evolution API provides a Swagger documentation interface:

- **Swagger UI**: http://localhost:8080/docs

## 🔗 Useful Links

- [Evolution API Documentation](https://doc.evolution-api.com/)
- [Evolution API GitHub](https://github.com/EvolutionAPI/evolution-api)
- [n8n Documentation](https://docs.n8n.io/)

## 📝 License

This setup is for personal/development use. Please refer to Evolution API's official licensing for production deployments.
