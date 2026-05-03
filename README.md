# Lab4 API CV

## Descripción

Este proyecto es una API REST desarrollada con FastAPI para el análisis de imágenes. Permite subir imágenes y obtener información básica como dimensiones y detección de bordes utilizando OpenCV.

## Características

- **Análisis de Imágenes**: Sube una imagen y obtén sus dimensiones (alto y ancho) y si se detectaron bordes.
- **API RESTful**: Construida con FastAPI para una experiencia rápida y moderna.
- **Procesamiento con OpenCV**: Utiliza algoritmos de visión por computadora para el análisis de imágenes.
- **Información de Dimensiones**: Obtención del alto y ancho de la imagen.
- **Gestión de Dependencias**: Utiliza Poetry para la gestión de paquetes.
- **Calidad de Código**: Integración con SonarCloud para análisis estático.


## Tecnologías Utilizadas

- **FastAPI**: Framework web para construir APIs con Python.
- **Poetry**: Herramienta de gestión de dependencias y empaquetado.
- **Uvicorn**: Servidor ASGI para ejecutar la aplicación.
- **OpenCV**: Biblioteca de visión por computadora para el procesamiento de imágenes.
- **NumPy**: Para operaciones numéricas.
- **Matplotlib**: Para visualización (aunque no se usa directamente en este proyecto).
- **Python-multipart**: Para manejar uploads de archivos.

## Instalación

1. Asegúrate de tener Python 3.11 o superior y Poetry instalado en el sistema.

2. Clona el repositorio:
   ```
   git clone <url-del-repositorio>
   cd Ucv-SI-lab4
   ```

3. Instala las dependencias usando Poetry:
   ```
   poetry install
   ```

4. Activa el entorno virtual:
   ```
   poetry shell
   ```

## Uso

1. Ejecuta el servidor:
   ```
   uvicorn src.lab4_api_cv.api.main:app --reload
   ```

2. La API estará disponible en `http://127.0.0.1:8000`.

### Documentación Interactiva

FastAPI proporciona documentación automática en:
- Swagger UI: `http://127.0.0.1:8000/docs`
- ReDoc: `http://127.0.0.1:8000/redoc`

## Endpoints de la API

### POST /analyze-image

Sube una imagen para analizarla.

- **Parámetros**:
  - `file`: Archivo de imagen (multipart/form-data).

- **Respuesta de Éxito (200):**
  ```json
  {
    "mensaje": "Procesamiento exitoso",
    "resultado": {
      "alto": 225,
      "ancho": 225,
      "bordes_detectados": 1
    }
  }
  ```
**Campos del Resultado:**
- `alto`: Altura de la imagen en píxeles.
- `ancho`: Ancho de la imagen en píxeles.
- `bordes_detectados`: 1 si se detectaron bordes, 0 en caso contrario
### GET /

Endpoint de salud para verificar que la API está funcionando.

**Respuesta:**
```json
{
  "mensaje": "Procesamiento exitoso"
}
```

## Pruebas

Para ejecutar las pruebas:

```
pytest tests/
```

## Estructura del Proyecto

```
Ucv-SI-lab4/
├── README.md
├── sonar-project.properties
├── src/
│   └── lab4_api_cv/
│       ├── pyproject.toml
│       ├── api/
│       │   └── main.py
│       ├── data/
│       │   └── descarga (2).jfif
│       └── services/
│           └── image_service.py
└── tests/
    └── test_api.py
```

## Autor

- **Josias Eliel Alfageme Neyra** - [jalfagemene@ucvvirtual.edu.pe](mailto:jalfagemene@ucvvirtual.edu.pe)

## Licencia

Este proyecto está bajo la Licencia MIT.

## Análisis del Proyecto

### Funcionalidad Principal

La funcionalidad principal se centra en el procesamiento de imágenes mediante la detección de bordes. El servicio `image_service.py` utiliza OpenCV para:

1. Leer la imagen en escala de grises.
2. Aplicar el filtro de Canny para detectar bordes.
3. Calcular si hay bordes presentes (basado en la suma de píxeles del resultado de Canny).
4. Devolver las dimensiones de la imagen.

### Arquitectura

- **Capa API**: `main.py` maneja las rutas HTTP y la subida de archivos.
- **Capa de Servicios**: `image_service.py` contiene la lógica de negocio para el análisis de imágenes.
- **Separación de Preocupaciones**: El código está modularizado para facilitar el mantenimiento y las pruebas.

### Mejoras Potenciales

- Agregar validación de tipos de archivos de imagen.
- Implementar manejo de errores más robusto.
- Expandir las funcionalidades de análisis (detección de objetos, OCR, etc.).
- Agregar logging para monitoreo.
- Mejorar las pruebas con casos más específicos.