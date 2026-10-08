# AI Direct Summit · Barcelona — Guía del asistente

Guía web independiente para los asistentes del AI Direct Summit Barcelona (8 de octubre de 2026, Palo Alto · Sala Cortés). No es una aplicación oficial del evento ni de su organizador.

Los datos proceden de `fuentes/evento-verificado.json` y están integrados en `index.html` sin cambios.

## Archivos

| Archivo | Uso |
|---|---|
| `index.html` | App completa y autocontenida (HTML, CSS, JS, iconos SVG y datos) |
| `manifest.webmanifest` | Manifiesto PWA (rutas relativas, `start_url` y `scope` = `./`) |
| `sw.js` | Service worker: cachea solo los archivos de esta app |
| `icon.svg`, `icon-180.png`, `icon-512.png` | Iconos (los PNG se generaron desde el SVG con `sips`) |
| `.nojekyll` | Evita el procesado Jekyll en GitHub Pages |

## Funciones

- **Agenda** con el estado en directo según la hora de Europe/Madrid (en curso, siguiente o finalizada), buscador sin acentos, filtros por categoría y guardadas, «Ocultar finalizadas» e «Ir a ahora».
- **Ficha de cada sesión**: guardar, `.ics`, compartir, notas privadas y navegación anterior/siguiente.
- **Mi agenda**: sesiones guardadas, notas de la jornada y por sesión, lugares guardados, y exportación a `.ics` y `.txt`.
- **Ponentes**: perfil con LinkedIn. Los participantes que la fuente no identifica se indican así, sin inventar nombres.
- **Lugar y rutas**: dirección, botón de copiar, rutas a pie, en transporte público o en coche (Google Maps) y Apple Maps. El mapa de OpenStreetMap solo se carga si el usuario lo pide.
- **Barcelona**: seis recomendaciones marcadas como selección editorial, con filtros, favoritos y ruta desde la sede.
- **Calendario**: jornada completa, programa completo o mi agenda.
- **Interfaz**: modo claro, oscuro o automático; compartir; «Descargar HTML»; guía honesta de «Añadir a inicio» por navegador.
- **Privacidad**: favoritos y notas se guardan en `localStorage` (prefijo `aids26:`) y nunca se envían a nadie.

## Publicar en GitHub Pages (subruta)

Sube el contenido de esta carpeta tal cual (sin `fuentes/` si no se quiere publicar). Todas las rutas son relativas, así que funciona en `https://usuario.github.io/repo/`.

## Uso sin conexión

- `index.html` descargado funciona abriéndolo directamente (`file://`). El service worker y la instalación solo funcionan sobre https.
- Los enlaces externos (mapas, LinkedIn, webs) necesitan conexión.

## Pruebas

- Para simular la hora, añade `?ahora=2026-10-08T12:40` (hora de Barcelona). La interfaz muestra la etiqueta «Simulada».
- Comprobado: sintaxis JS (`node --check`), que los datos integrados son idénticos al JSON fuente, que todos los iconos y acciones referenciados existen, y la lógica temporal, el formato `.ics` (UTC, escapado, plegado a 75 bytes) y el buscador.
- Revisión real en Chrome: siete secciones a 320, 390 y 768 px sin desbordamiento horizontal; búsqueda sin tildes, favoritos y notas persistentes tras recarga, descarga de HTML y .ics con nueve sesiones y UTC correcto. Recarga de la app con el servidor local detenido: correcta mediante caché.
- No se ha probado instalación en un teléfono físico. La apertura directa file:// está bloqueada por el navegador de pruebas; el HTML descargado se revisa en HTTP local aislado.
