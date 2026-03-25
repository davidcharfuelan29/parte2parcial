# Parte2Parcial

Este repositorio contiene un microservicio en Python usando FastAPI para exponer un endpoint que llama a la API de Google Gemini (Google Generative AI).

## Descripción

El servicio tiene un único endpoint:

- `GET /llm/{prompt}`

Recibe un texto (`prompt`) por URL, lo envía a `google.genai.Client().models.generate_content(...)` usando el modelo `gemini-3-flash-preview`, y devuelve una respuesta JSON con el texto generado.

## Archivos

- `main.py`: aplicación FastAPI con el endpoint.
- `requirements.txt`: dependencias del proyecto.
- `README.md`: esta documentación.

## Requisitos

- Python 3.11+ (preferible)
- Dependencias listadas en `requirements.txt`.
- Variable de entorno `GEMINI_API_KEY` con la clave de Google generative AI.

## Instalación

1. Clonar el proyecto:

```bash
git clone https://github.com/davidcharfuelan29/parte2parcial.git
cd parte2parcial
```

2. Crear e instalar entorno virtual:

```bash
python -m venv .venv
source .venv/bin/activate
pip install --upgrade pip
pip install -r requirements.txt
```

3. Configurar la clave en `.env` (opcional; también puede estar en el entorno):

```
GEMINI_API_KEY=tu_valor_de_api_key
```

## Uso

Ejecutar el servidor:

```bash
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

Llamar al endpoint con prompt en la ruta:

```bash
curl "http://127.0.0.1:8000/llm/Hola%20mundo"
```

Respuesta esperada:

```json
{"Respuesta": "...texto generado por Gemini..."}
```

## Notas

- El proyecto asume que la librería `google.genai` está instalada (incluida en requirements).
- Si usas un entorno sin `python-dotenv`, asegúrate de exportar `GEMINI_API_KEY` antes de iniciar el servidor.

## Mejoras sugeridas

- Agregar manejo de errores y validación del prompt.
- Soportar consultas POST con JSON.
- Agregar pruebas unitarias para el endpoint y el cliente de API.
