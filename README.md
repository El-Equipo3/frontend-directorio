# Directorio Académico — Frontend (Interfaz Web)

Interfaz web de página única (SPA simple) construida con **HTML, CSS y JavaScript puro** (sin frameworks ni dependencias). Permite gestionar de forma visual docentes, materias y la asignación de materias a docentes, consumiendo la API REST del backend.

Este repositorio contiene únicamente la interfaz. La lógica y los datos viven en el repositorio del backend (Flask + MySQL).

---

## ¿Para qué sirve?

Ofrece un panel de administración con tres secciones, navegables desde un menú lateral:

- **Docentes** — alta, listado, edición y borrado de profesores (nombre y correo).
- **Materias** — alta, listado, edición y borrado de asignaturas (clave, nombre y créditos).
- **Asignaciones** — vincular o desvincular materias a un docente, y consultar las materias que imparte cada docente.

---

## ¿Cómo funciona?

- Es un **único archivo `index.html`** que incluye todo: estructura, estilos (CSS embebido) y lógica (JavaScript embebido). No requiere compilación ni instalación de paquetes.
- Toda la comunicación con el servidor se hace con la **API Fetch** (`fetch`) contra los endpoints REST del backend.
- La navegación entre secciones se resuelve mostrando/ocultando bloques (`view-section`) sin recargar la página.
- Incluye un **sistema de alertas** flotantes que confirma operaciones exitosas o muestra errores devueltos por la API.
- Las tablas se rellenan dinámicamente con los datos recibidos del backend.

### Secciones de la interfaz

| Sección | Qué hace |
|---------|----------|
| **Docentes** | Tabla de docentes + formulario para crear o editar. Botones "Editar" y "Eliminar" por fila. |
| **Materias** | Tabla de materias + formulario para crear o editar. Botones "Editar" y "Eliminar" por fila. |
| **Asignaciones** | Selector para ver las materias de un docente, y formulario para vincular un docente con una materia. Permite "Desasignar". |

---

## Requisitos previos

- El **backend** debe estar en ejecución y accesible (ver el repositorio del backend).
- Un **navegador web** moderno (Chrome, Firefox, Edge, Safari).
- Opcionalmente, un servidor estático sencillo para servir el archivo (recomendado frente a abrirlo con `file://`).

---

## Configuración

Antes de usarlo, ajusta la URL de la API. En `index.html`, dentro de la etiqueta `<script>`, está la constante:

```javascript
const API_URL = 'https://jubilant-lamp-wvr6qjqwj6v92g46g-3000.app.github.dev/api/v1';
```

Cámbiala por la dirección donde corra tu backend. Por ejemplo, en desarrollo local:

```javascript
const API_URL = 'http://localhost:3000/api/v1';
```

> Si el frontend y el backend están en orígenes distintos, el backend ya tiene **CORS habilitado** para todos los orígenes, por lo que las peticiones funcionarán sin configuración adicional.

---

## Cómo ejecutarlo

No requiere instalación de dependencias. Tienes varias opciones:

### Opción 1 — Abrir directamente

Haz doble clic en `index.html` o ábrelo desde el navegador con `Archivo → Abrir`.

> Funciona, pero algunos navegadores aplican restricciones a las peticiones desde `file://`. Si tienes problemas, usa la Opción 2.

### Opción 2 — Servirlo con un servidor estático (recomendado)

Desde la carpeta del repositorio:

```bash
# Con Python (ya viene instalado en la mayoría de sistemas)
python -m http.server 8080
```

Luego abre en el navegador:

```
http://localhost:8080
```

Otras alternativas equivalentes:

```bash
# Con Node.js
npx serve

# Con la extensión "Live Server" de VS Code
# (clic derecho sobre index.html → "Open with Live Server")
```

---

## Flujo de uso

1. Asegúrate de que el **backend esté corriendo** y de que `API_URL` apunte a él.
2. Abre el frontend en el navegador.
3. Al cargar, la app trae automáticamente la lista de docentes y materias.
4. Usa el menú lateral para moverte entre **Docentes**, **Materias** y **Asignaciones**.
5. Crea, edita o elimina registros desde cada sección.

---

## Solución de problemas

| Síntoma | Posible causa / solución |
|---------|--------------------------|
| "Error al conectar con el servidor" | El backend no está corriendo o `API_URL` es incorrecta. |
| Las tablas aparecen vacías | No hay datos aún, o la API no responde. Revisa la consola del navegador (F12). |
| Errores de CORS en consola | Verifica que el backend tenga CORS habilitado y que la URL/puerto sean correctos. |
| Cambios no se reflejan | Refresca con `Ctrl/Cmd + Shift + R` para limpiar la caché. |

---

## Estructura del proyecto

```
.
└── index.html   # Toda la aplicación: HTML + CSS + JavaScript
```

---

## Notas

- No usa frameworks ni librerías externas: solo HTML, CSS y JavaScript nativos.
- El diseño es responsivo: en pantallas menores a 900px las columnas se apilan.
- Pensado como cliente del backend "Directorio Académico"; no funciona de forma aislada sin la API.
