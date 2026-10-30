Explorador web Interactivo de Rick and Morty
Integrante
Carlos Ayala alias "CD-Athern"
Descripción
Portal·Dex consume datos reales con `fetch()`. Cada página trae 20 personajes con foto, nombre, estado, especie y una descripción generada a partir de sus datos (origen, última ubicación y episodios). El diseño es asimétrico y colorido, con tarjetas inclinadas, un portal animado y sombras duras.


El proyecto está construido como una aplicación estática, sin servidor propio ni dependencias externas que deban instalarse. La información de los personajes se obtiene en tiempo real desde la API.

Funcionalidades
Consulta de personajes mediante fetch().
Visualización de imagen, nombre, estado, especie y última ubicación.
Búsqueda por nombre.
Filtros por estado y especie.
Paginación de resultados.
Gestión de favoritos.
Persistencia de favoritos mediante localStorage.
Mensajes para carga, resultados vacíos, errores de red y errores de la API.
Diseño responsive para celulares, tablets y computadoras.
Etiquetas semánticas y estados accesibles mediante atributos ARIA.
Tecnologías utilizadas
HTML5.
CSS3 y diseño responsive.
JavaScript vanilla (ES6+).
Rick and Morty API.
GitHub Pages.
Instrucciones de uso
Opción 1: abrir localmente
Descarga o clona este repositorio:

git clone https://github.com/CD-Athern/proyecto-web-ia.git
1. Abre la página; los personajes cargan solos.
2. Escribe en **Buscar por nombre** o usa los filtros de **Estado**, **Género** y **Especie**.
3. Usa **Ordenar página** para ver A → Z o Z → A.
4. Toca el ♥ de una tarjeta para guardarla; revisa tu colección en la pestaña **Favoritos**.
5. Navega con **Anterior / Siguiente**.
6. El botón circular de la esquina cambia entre modo oscuro y claro (se recuerda tu elección).

No es necesario instalar paquetes ni ejecutar un servidor local. Se requiere conexión a Internet para consultar la API. Los favoritos se guardan en el localStorage del navegador y pueden desaparecer si se borran los datos del sitio.

Opción 2: versión publicada
También puede utilizarse la versión publicada en GitHub Pages cuando esté habilitada para el repositorio.

 Estructura

```
proyecto-web-ia/
├── index.html   # estructura de la página
├── style.css    # diseño, temas y adaptabilidad
├── script.js    # fetch, búsqueda, filtros, favoritos, tema
└── README.md
```
Prompts utilizados durante el desarrollo
Prompt 1 — Generación inicial
> «Crea una página web que consulte la API de Rick and Morty con fetch(),debe mostrar al menos 15 personajes con imagen y descripción, debe tener buscador, filtros, favoritos guardados en localStorage, mensajes cuando no haya resultados o falle la consulta, y sea adaptable a celular y computadora. Que la interfaz sea profesional sin sobrecargar. Todo el código y los textos en español.»

*Resultado:* los tres archivos base. Sirvió para tener una estructura completa que luego revisamos función por función.

Prompt 2 — Entender el código**
> «Explícame línea por línea qué hace `consultarPersonajes()` y por qué se usa `async/await` en lugar de `.then()`. Quiero poder explicarlo de manera sencilla.

Prompt 3 — Mejora concreta
Si escribo rápido en el buscador salen resultados de una búsqueda vieja encima de la nueva. ¿Cómo lo evito?
 se agregó `AbortController` para cancelar la petición anterior y el retraso (`retrasar`) de 400 ms en el buscador.

Dificultades encontradas y soluciones
Manejo de búsquedas sin resultados
La API responde con código HTTP 404 cuando una búsqueda no encuentra personajes. Se agregó una comprobación de response.ok para mostrar un mensaje comprensible en lugar de dejar la interfaz en un estado ambiguo.


error encontrado y cómo lo resolvimos

**Error:** al buscar un nombre inexistente (por ejemplo «zzzz») la página mostraba «falló la consulta» en vez de «sin resultados».
**Causa:** la API responde con código **404** cuando no hay coincidencias. `fetch()` no lanza error con un 404, pero la validación `if (!respuesta.ok)` sí lo trataba como fallo.
**Solución:** revisar `respuesta.status === 404` **antes** de la validación general y mostrar el mensaje «Sin resultados». Así se distingue entre «no hay datos» (404) y «algo falló» (red caída, error 500).


Aprendizajes
El desarrollo permitió practicar el consumo de una API externa, la gestión de estados en JavaScript, la persistencia en el navegador, el manejo explícito de errores y la creación de una interfaz responsive. También se comprobó que las respuestas generadas por IA deben validarse contra la documentación de la API, el comportamiento real de la aplicación y los requisitos del proyecto.
