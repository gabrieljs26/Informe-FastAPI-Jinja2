# Sistema de Reporte de Tareas con FastAPI y Jinja2

Este proyecto implementa una aplicación web basada en el patrón Modelo-Vista-Controlador (MVC) simplificado, utilizando **FastAPI** para el backend y **Jinja2** para el renderizado de plantillas en el servidor. El sistema permite la visualización, filtrado y análisis estadístico de una lista de tareas predefinida.

## Arquitectura y Componentes

El funcionamiento del sistema se divide en tres componentes técnicos principales:

### 1. Lógica del Servidor (Backend - `main.py`)
Este archivo actúa como el controlador de la aplicación. Sus responsabilidades incluyen:
*   **Inicialización de la App:** Configura la instancia de `FastAPI` y el directorio de archivos estáticos/plantillas.
*   **Gestión de Datos:** Contiene la estructura de datos en memoria (`TAREAS`) y aplica la lógica de negocio para filtrar estos datos según las peticiones del cliente.
*   **Enrutamiento:** Define los endpoints (como `/` y `/informe`) y asocia las funciones que procesarán cada petición HTTP.
*   **Renderizado de Respuesta:** Utiliza `TemplateResponse` para combinar los datos procesados con las plantillas HTML y devolver una respuesta completa al navegador.

### 2. Motor de Plantillas (Frontend - `templates/`)
La capa de presentación utiliza **Jinja2** para generar HTML dinámico.
*   **Interpolación de Variables:** Utiliza la sintaxis `{{ variable }}` para inyectar datos enviados desde el servidor (por ejemplo, totales, listas de tareas o valores de configuración).
*   **Estructuras de Control:** Emplea etiquetas como `{% for %}` y `{% if %}` para iterar sobre listas de datos o mostrar elementos condicionalmente directamente en el HTML.
*   **Herencia de Plantillas:** Permite modularizar el código HTML (ej. `base.html` contiene la estructura común) para mantener el código limpio y reutilizable.

### 3. Parámetros de Consulta (Query Parameters)
La interacción entre el usuario y el servidor para el filtrado de datos se realiza mediante parámetros en la URL (Query Strings).
*   **Funcionamiento:** Al realizar una petición GET (ej: `/informe?estado=pendiente&min_prioridad=4`), los datos se codifican en la URL.
*   **Validación en FastAPI:** La función del controlador declara argumentos (`estado`, `min_prioridad`) utilizando la clase `Query`. Esto permite a FastAPI leer, convertir tipos de datos (como `int`) y validar la entrada automáticamente antes de ejecutar la lógica de filtrado.

---

## Instrucciones de Ejecución

### Prerrequisitos
Se requiere tener Python instalado. Las dependencias del proyecto se instalan mediante:
```bash
pip install -r requirements.txt
# O alternativamente:
pip install fastapi uvicorn jinja2
```

### Despliegue Local
Para iniciar el servidor de desarrollo, ejecute el siguiente comando en la terminal:
```bash
uvicorn main:app --reload
```
*   **main**: Hace referencia al módulo `main.py`.
*   **app**: Hace referencia a la instancia de la aplicación FastAPI dentro del módulo.
*   **--reload**: Habilita la recarga automática del servidor ante cambios en el código.

### Acceso
Una vez iniciado el servidor, la aplicación estará disponible en:
[http://127.0.0.1:8000/informe](http://127.0.0.1:8000/informe)

---

## Estructura del Proyecto

*   **`main.py`**: Punto de entrada de la aplicación. Contiene la lógica de enrutamiento y procesamiento de datos.
*   **`templates/`**: Directorio de plantillas HTML.
    *   `base.html`: Plantilla base con la estructura HTML común.
    *   `informe.html`: Plantilla específica para la vista de reportes y gráficos.
*   **`requirements.txt`**: Archivo de especificación de dependencias del proyecto.
