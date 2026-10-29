# Ruka Kalen — Sitio web

Landing informativa de **Ruka Kalen — Centro Terapéutico**, en Lomas Coloradas,
San Pedro (Diguillín 478).

Una sola página que presenta las cuatro especialidades —Psicología, Terapia
Ocupacional, Fonoaudiología y Kinesiología— y deriva al WhatsApp para agendar.
No tiene backend, no guarda datos de pacientes y no usa cookies, analítica ni
servicios de terceros.

**Sitio en línea:** https://yeyobitz.github.io/ruka-kalen/ *(dirección provisoria)*

## Ficha técnica

| | |
|---|---|
| Tecnología | HTML5 + CSS3 estático (sin WordPress, sin frameworks) |
| JavaScript | Ninguno propio (solo datos estructurados JSON-LD) |
| Backend / base de datos | No tiene |
| Dependencias externas | Ninguna: fuentes e imágenes se sirven desde el mismo sitio |
| Peso total | ~340 KB en 21 archivos |
| Requisitos del hosting | Servir archivos estáticos y HTTPS (Apache, Nginx, cPanel, Pages, Netlify…) |
| Navegadores | Chrome, Edge, Firefox y Safari actuales (móvil y escritorio) |

## Estructura

```
.
├── index.html              Página principal
├── privacidad.html         Aviso de privacidad
├── 404.html                Página de error
├── robots.txt              Indexación
├── .htaccess               Configuración opcional para Apache
├── .nojekyll               Necesario para GitHub Pages
├── assets/
│   ├── css/styles.css      Estilos
│   ├── brand/              Imagotipo y personitas (SVG)
│   ├── fonts/              Amsi Pro y Myriad Pro (woff2)
│   ├── favicon.svg
│   ├── apple-touch-icon.png
│   └── og.jpg              Imagen al compartir por WhatsApp/redes
└── DEPLOY.md               Guía de publicación y mantenimiento
```

## Ver el sitio localmente

No requiere instalación ni compilación:

```bash
python3 -m http.server 8123
# Abrir http://127.0.0.1:8123/
```

También se puede abrir `index.html` directamente en el navegador, aunque el
servidor local reproduce mejor las condiciones del hosting.

## Publicar

- **Hosting propio (Apache/cPanel):** subir el contenido a `public_html`,
  activar HTTPS y listo. Pasos detallados en [`DEPLOY.md`](DEPLOY.md).
- **GitHub Pages:** publicar desde la rama `gh-pages`. Ya está configurado.

## Cambiar datos de contacto

El número de WhatsApp está en los enlaces `wa.me` y se repite en varios
botones. Para reemplazarlo por el definitivo:

1. Buscar `56950944500` (formato del enlace) y reemplazar por el nuevo número
   sin `+`, sin espacios y sin guiones.
2. Buscar `+56 9 5094 4500` (texto visible) y reemplazar por el número con
   formato legible.

También conviene actualizar:

- Correo: `contacto.rukakalen@gmail.com`
- Dirección: `Diguillín 478, Lomas Coloradas, San Pedro`
- Enlaces de Google Maps (`google.com/maps/search`)
- Al cambiar de dominio: `og:url` y `og:image` en `index.html`.

## Privacidad

El sitio no tiene formularios, cuentas, cookies ni rastreo. El único enlace
externo es el botón de WhatsApp, que se abre solo si la persona lo toca. El
detalle está en `privacidad.html`.

## Tipografías

Se usan **Amsi Pro** (títulos) y **Myriad Pro** (texto), entregadas por el
cliente junto al manual de marca. Son fuentes comerciales: su publicación como
webfont requiere la licencia de webfont correspondiente, responsabilidad del
cliente.

## Créditos

Diseño y desarrollo: Diego Quiñones.
Identidad visual y tipografías: entregadas por el cliente.
