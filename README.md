# API de Chistes — Deploy en Azure (Programación 4)

API en .NET 10 que consume la API pública de chistes (`official-joke-api.appspot.com`) usando `IHttpClientFactory`.
Es la API de la Unidad 5 (paso 1), preparada para deployar en **Azure App Service**. No usa base de datos.

## Estructura

| Proyecto | Qué contiene |
| --- | --- |
| `Application` | Interfaz `IJokeService` y el DTO `JokeDTO` |
| `Infrastructure` | `JokeService`: llama a la API externa con el cliente `"jokes"` |
| `Presentation` | La Web API: `Program.cs`, `JokesController` y configuración |

## Correr en local

```bash
dotnet run --project Presentation --launch-profile http
```

Se abre Swagger en `http://localhost:5100/swagger`.

## Endpoints

| Ruta | Qué hace |
| --- | --- |
| `GET /api/jokes/random` | Un chiste aleatorio |
| `GET /api/jokes/{id}` | Chiste por id (404 si no existe) |
| `GET /api/jokes/types` | Tipos de chistes |
| `GET /api/jokes/ten` | Diez chistes aleatorios |
| `GET /api/jokes/random/{cantidad}` | N chistes aleatorios |
| `GET /api/jokes/type/{type}` | Chistes de un tipo (por ejemplo `programming`) |

## Configuración

La URL de la API externa está en `Presentation/appsettings.json`, en `ExternalApis:Jokes`.
En Azure se puede reemplazar sin tocar el código: **Settings → Environment variables → App settings**, con el nombre `ExternalApis__Jokes`.

## Deploy

1. Crear una Web App con runtime **.NET 10 (LTS)**, Windows y plan **Free F1**.
2. **Deployment Center → Source: GitHub** → este repo, rama `main` → Save.
3. Azure agrega un workflow en `.github/workflows/`; cada push a `main` deploya la API.
4. Abrir la URL de la Web App: redirige a Swagger.
