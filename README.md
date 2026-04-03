# Filmaffinity Ratings API (Render-ready)

Este repositorio incluye una API Flask lista para desplegar en Render.

## Endpoints
- `/health`
- `/api/userratings?user_id=731957`
- `/api/userratings.csv?user_id=731957`
- `/api/userratings.view?user_id=731957`
- `DELETE /api/cache/userratings?user_id=731957`
- `POST /api/cache/clear-cooldown`

## Opción 1: desplegar en Render usando Dockerfile del repo
En Render:
- New > Web Service
- Source: GitHub
- Selecciona este repo
- **Language:** Docker
- **Dockerfile Path:** `./Dockerfile` (o déjalo vacío si Render lo detecta en la raíz)
- **Instance Type:** Free

## Opción 2: desplegar como Python nativo (sin Docker)
En Render:
- New > Web Service
- Source: GitHub
- **Language:** Python 3
- **Build Command:** `pip install -r requirements.txt`
- **Start Command:** `gunicorn app:app`
- **Instance Type:** Free

## Notas
- La caché es en memoria del proceso (sin Google Cloud / Firestore).
- Si Render duerme el servicio gratuito, la caché se perderá al reactivarse.
- Si Filmaffinity aplica anti-bot o rate limiting, la API puede recibir 429 desde el upstream.
