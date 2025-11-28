# 🎓 Chatbot Educativo UNAB - IA Mentor

<div align="center">

![Python](https://img.shields.io/badge/Python-3.9%2B-3776AB?style=for-the-badge&logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-0.109-009688?style=for-the-badge&logo=fastapi&logoColor=white)
![LangChain](https://img.shields.io/badge/LangChain-RAG-7C3AED?style=for-the-badge&logo=chainlink&logoColor=white)
![Ollama](https://img.shields.io/badge/Ollama-Llama%203-FF6B35?style=for-the-badge&logo=meta&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-Compose-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-8.0-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)

**Asistente académico inteligente con RAG (Retrieval-Augmented Generation) y LLM local**

[Características](#-características) •
[Arquitectura](#-arquitectura) •
[Instalación](#-instalación) •
[API](#-api-endpoints) •
[Contribuir](#-contribución)

</div>

---

## 📖 Descripción

Sistema de chatbot educativo diseñado para asistir a estudiantes universitarios mediante inteligencia artificial. Utiliza **Retrieval-Augmented Generation (RAG)** para proporcionar respuestas contextualizadas basadas en material académico, y modelos de lenguaje locales (**Ollama**) para garantizar privacidad total de los datos.

### 🎯 Caso de Uso Principal
Asistencia académica para el curso "Fundamentos de Inteligencia Artificial" (CINF103) de la Universidad Andrés Bello, Santiago, Chile.

---

## ✨ Características

### 🧠 Sistema RAG Avanzado
- **ChromaDB**: Base de datos vectorial para búsqueda semántica
- **Embeddings locales**: Procesamiento de PDFs académicos
- **Respuestas contextualizadas**: Basadas en el material del curso

### 🤖 IA Local y Privada
- **Ollama Integration**: Soporte para Llama 3, Mistral, CodeLlama
- **Sin APIs externas**: Funciona completamente offline
- **Privacidad total**: Datos procesados localmente

### ⚡ Arquitectura de Alto Rendimiento
- **Celery + Redis**: Procesamiento asíncrono distribuido
- **SSE Streaming**: Respuestas en tiempo real palabra por palabra
- **Escalabilidad horizontal**: Múltiples workers concurrentes
- **Optimización GPU**: Configurado para RTX 3060 12GB

### 👤 Gestión de Usuarios
- **JWT Authentication**: Autenticación segura con tokens
- **Sesiones persistentes**: Historial por usuario en MySQL
- **Sistema de feedback**: Calificación 5 estrellas para respuestas

### 📊 Dashboard de Analytics
- **Métricas en tiempo real**: Estadísticas de uso
- **Sistema de diagnóstico**: Stress testing integrado
- **Exportación de reportes**: Excel y JSON

### 🎨 Frontend Moderno
- **Dark/Light Mode**: Tema adaptativo
- **Markdown Rendering**: Respuestas formateadas
- **Responsive Design**: Optimizado para móvil y desktop
- **Cloudflare Turnstile**: Protección anti-bot

---

## 🏗 Arquitectura

```
┌─────────────────────────────────────────────────────────────────────┐
│                          FRONTEND (Nginx)                            │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐                  │
│  │  Chat UI    │  │  Dashboard  │  │   Login     │                  │
│  │  (SSE)      │  │  (Charts)   │  │   (JWT)     │                  │
│  └──────┬──────┘  └──────┬──────┘  └──────┬──────┘                  │
└─────────┼────────────────┼────────────────┼─────────────────────────┘
          │                │                │
          └────────────────┼────────────────┘
                           ▼
┌─────────────────────────────────────────────────────────────────────┐
│                      BACKEND (FastAPI)                               │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌────────────┐  │
│  │  Auth API   │  │  Chat API   │  │ Dashboard   │  │ Diagnostics│  │
│  │  (JWT)      │  │  (RAG)      │  │    API      │  │    API     │  │
│  └──────┬──────┘  └──────┬──────┘  └──────┬──────┘  └─────┬──────┘  │
│         │                │                │               │         │
│         ▼                ▼                ▼               ▼         │
│  ┌──────────────────────────────────────────────────────────────┐   │
│  │                    AI System (RAG Pipeline)                   │   │
│  │  ┌────────────┐  ┌────────────┐  ┌────────────────────────┐  │   │
│  │  │  Embeddings│  │  Vector    │  │  LangChain + Ollama    │  │   │
│  │  │  (HuggingF)│  │  Search    │  │  (Llama 3)             │  │   │
│  │  └────────────┘  └────────────┘  └────────────────────────┘  │   │
│  └──────────────────────────────────────────────────────────────┘   │
└─────────┬─────────────────────┬─────────────────────┬───────────────┘
          │                     │                     │
          ▼                     ▼                     ▼
┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐
│     MySQL       │  │    ChromaDB     │  │     Redis       │
│   (Usuarios,    │  │  (Vectores,     │  │   (Celery,      │
│   Sesiones,     │  │   Embeddings)   │  │    Cache)       │
│   Feedback)     │  │                 │  │                 │
└─────────────────┘  └─────────────────┘  └─────────────────┘
```

---

## 🛠 Stack Tecnológico

| Categoría | Tecnologías |
|-----------|-------------|
| **Backend** | FastAPI, LangChain, SQLAlchemy, Celery |
| **IA/ML** | Ollama (Llama 3), ChromaDB, HuggingFace Embeddings |
| **Base de Datos** | MySQL 8.0, Redis |
| **Frontend** | HTML5, CSS3, JavaScript (Vanilla), Marked.js |
| **DevOps** | Docker, Docker Compose, Nginx |
| **Seguridad** | JWT, bcrypt, Cloudflare Turnstile |

---

## 📦 Instalación

### Prerrequisitos

- Python 3.9+
- MySQL 8.0+
- Redis
- [Ollama](https://ollama.com/) instalado
- Docker & Docker Compose (opcional)

### Opción 1: Instalación Manual

```bash
# 1. Clonar repositorio
git clone https://github.com/HakimRabi/chatbot-educativo.git
cd chatbot-educativo

# 2. Crear entorno virtual
python -m venv venv
# Windows
venv\Scripts\activate
# Linux/macOS
source venv/bin/activate

# 3. Instalar dependencias
pip install -r requirements.txt

# 4. Configurar variables de entorno
cp .env.example .env
# Editar .env con tus credenciales

# 5. Instalar modelo Ollama
ollama pull llama3

# 6. Iniciar MySQL y crear base de datos
mysql -u root -p < init-db.sql

# 7. Iniciar aplicación
cd backend
uvicorn app:app --host 0.0.0.0 --port 8000 --reload
```

### Opción 2: Docker Compose

```bash
# 1. Clonar y configurar
git clone https://github.com/HakimRabi/chatbot-educativo.git
cd chatbot-educativo
cp .env.example .env
# Editar .env con tus credenciales

# 2. Construir e iniciar
docker-compose up -d --build

# 3. Verificar servicios
docker-compose ps
```

---

## ⚙️ Configuración

### Variables de Entorno

Copia `.env.example` a `.env` y configura:

```env
# Base de Datos
DB_HOST=localhost
DB_PORT=3306
DB_NAME=chatbot
DB_USER=root
MYSQL_PASSWORD=tu_password_seguro

# Seguridad
SECRET_KEY=tu_secret_key_unico  # Genera con: python -c "import secrets; print(secrets.token_urlsafe(64))"

# Ollama
OLLAMA_HOST=http://127.0.0.1:11434
OLLAMA_MODEL=llama3

# Redis/Celery
CELERY_BROKER_URL=redis://localhost:6379/0
```

### Documentos PDF

Coloca los documentos académicos en `backend/data/pdfs/`. El sistema los indexará automáticamente al iniciar.

---

## 🚀 Uso

### Acceso a la Aplicación

| Servicio | URL |
|----------|-----|
| **Chat** | http://localhost:8000 |
| **Login** | http://localhost:8000/pages/login.html |
| **Dashboard** | http://localhost:8000/pages/dashboard.html |
| **API Docs** | http://localhost:8000/docs |
| **ReDoc** | http://localhost:8000/redoc |

### Scripts de Inicio (Windows)

```batch
# Iniciar API
startAPI.bat

# Iniciar Worker Celery
start_worker.bat
```

---

## 📚 API Endpoints

### Autenticación

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| `POST` | `/auth/register` | Registro de usuarios |
| `POST` | `/auth/login` | Inicio de sesión (JWT) |
| `POST` | `/auth/logout` | Cerrar sesión |

### Chat

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| `POST` | `/preguntar` | Enviar pregunta (SSE streaming) |
| `GET` | `/api/sessions` | Listar sesiones del usuario |
| `POST` | `/api/sessions` | Crear nueva sesión |
| `DELETE` | `/api/sessions/{id}` | Eliminar sesión |

### Dashboard

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| `GET` | `/api/dashboard/stats` | Estadísticas generales |
| `GET` | `/api/dashboard/metrics` | Métricas del sistema |

### Diagnósticos

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| `POST` | `/api/diagnostics/stress-test` | Iniciar stress test |
| `GET` | `/api/diagnostics/status/{id}` | Estado del test |
| `GET` | `/api/diagnostics/report/{id}` | Obtener reporte |

---

## 📁 Estructura del Proyecto

```
chatbot-educativo/
├── backend/
│   ├── app.py                 # FastAPI principal
│   ├── ai_system.py           # Pipeline RAG
│   ├── auth.py                # Autenticación JWT
│   ├── chat.py                # Lógica de chat
│   ├── config.py              # Configuración
│   ├── dashboard.py           # Endpoints dashboard
│   ├── models.py              # Modelos SQLAlchemy
│   ├── diagnostics/           # Sistema de diagnóstico
│   │   ├── stress_runner.py
│   │   └── report_generator.py
│   └── data/                  # Datos (ignorado en git)
│       ├── pdfs/              # Documentos fuente
│       └── chroma_db/         # Base vectorial
├── frontend/
│   ├── index.html             # Chat principal
│   ├── pages/
│   │   ├── login.html
│   │   └── dashboard.html
│   └── assets/
│       ├── css/
│       └── js/
├── docker-compose.yml
├── requirements.txt
├── .env.example               # Template de configuración
└── README.md
```

---

## 🧪 Testing

### Ejecutar Tests

```bash
# Tests unitarios
pytest tests/ -v

# Con cobertura
pytest tests/ --cov=backend --cov-report=html
```

### Stress Testing

El sistema incluye un módulo de diagnóstico para stress testing accesible desde el Dashboard.

---

## 🐳 Docker

### Servicios Disponibles

```yaml
services:
  backend:     # API FastAPI (puerto 8000)
  frontend:    # Nginx (puerto 80)
  mysql:       # Base de datos (puerto 3306)
  redis:       # Cache/Broker (puerto 6379)
  worker:      # Celery worker
```

### Comandos Útiles

```bash
# Ver logs
docker-compose logs -f backend

# Reconstruir servicio específico
docker-compose up -d --build backend

# Escalar workers
docker-compose up -d --scale worker=3
```

---

## 🔒 Seguridad

### Medidas Implementadas

- ✅ JWT con expiración configurable
- ✅ Passwords hasheados con bcrypt
- ✅ CORS configurado
- ✅ Rate limiting
- ✅ Cloudflare Turnstile (anti-bot)
- ✅ Variables de entorno para secretos

### ⚠️ Importante

- **NUNCA** commits archivos `.env` o credenciales
- Usa el archivo `.gitignore` incluido
- Rota las credenciales periódicamente
- En producción, usa HTTPS

---

## 🤝 Contribución

¡Las contribuciones son bienvenidas!

1. Fork el proyecto
2. Crea una rama (`git checkout -b feature/nueva-funcionalidad`)
3. Commit cambios (`git commit -m 'Agrega nueva funcionalidad'`)
4. Push (`git push origin feature/nueva-funcionalidad`)
5. Abre un Pull Request

### Roadmap

- [ ] Soporte multi-idioma
- [ ] Integración con LMS (Moodle, Canvas)
- [ ] App móvil (React Native)
- [ ] Voice-to-text
- [ ] Análisis de sentimientos en feedback

---

## 📄 Licencia

Este proyecto está bajo la Licencia MIT. Ver [LICENSE](LICENSE) para más detalles.

---

## 👥 Autores

<table>
  <tr>
    <td align="center">
      <b>Luis Marcano</b><br>
      <sub>Desarrollador</sub>
    </td>
    <td align="center">
      <b>Hakim Rabi</b><br>
      <sub>Desarrollador</sub>
    </td>
    <td align="center">
      <b>Luciano Aguilar</b><br>
      <sub>Desarrollador</sub>
    </td>
  </tr>
</table>

### 🏛️ Universidad Andrés Bello - Chile
**Proyecto de Título - Ingeniería Civil Informática (2025)**

---

## 📞 Contacto

- 🔗 **Repositorio**: [github.com/HakimRabi/chatbot-educativo](https://github.com/HakimRabi/chatbot-educativo)
- 🏫 **Universidad**: [unab.cl](https://www.unab.cl/)

---

<div align="center">

**Desarrollado con ❤️ para la comunidad educativa**

*© 2025 - Proyecto de Título UNAB*

</div>
