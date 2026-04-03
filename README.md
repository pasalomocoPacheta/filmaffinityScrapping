# Filmaffinity Scraper API

Esta es una API construida con Flask y Python que extrae información de películas y series desde FilmAffinity. Devuelve respuestas en formato JSON. Utiliza `cloudscraper` para sortear la protección anti-bot y `BeautifulSoup` para el web scraping. Está configurada para poder desplegarse sin problemas en plataformas como Render.

## Endpoints Disponibles

- `GET /`
  Devuelve el estado de la API e información general.

- `GET /api/search?query={texto}`
  **Ejemplo:** `/api/search?query=avatar`
  Busca películas o series por nombre en FilmAffinity. Devuelve una lista de resultados con información básica (título, imagen, rating, año) y el ID de la película necesario para obtener más detalles.

- `GET /api/film?id={id}`
  **Ejemplo:** `/api/film?id=495604`
  Obtiene la información detallada completa (director, reparto, duración, géneros, etc.) de una película o serie usando su código interno de FilmAffinity.

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

## Notas Importantes
- Esta versión de la aplicación está diseñada para funcionar mediante scraping en vivo, no usa base de datos ni caché interna.
- Debido a las medidas de seguridad de FilmAffinity (como Cloudflare), esta aplicación hace uso esencial de `cloudscraper`.
- Si la aplicación empieza a comportarse mal o devuelve errores (ej. `filmaffinity error: 403`), puede deberse a que FilmAffinity ha reforzado las medidas anti-bot o si Render (u otro host) ha baneado IPs.
- Si el proyecto se levanta recién (como en el modo gratuito de Render), la primera petición podría tardar un poco mientras inicializa el scrapper.
