# Guía de publicación y mantenimiento

Documento para quien administre el sitio de Ruka Kalen. Cubre la publicación en
un hosting propio, la publicación con GitHub Pages, la verificación posterior y
cómo actualizar contenidos.

---

## 1. Antes de publicar

Revisar estos puntos, sobre todo la primera vez:

- [ ] **WhatsApp definitivo.** El sitio usa un número provisorio
  (`56950944500`). Reemplazarlo en todos los enlaces y en el texto visible
  (ver sección 6).
- [ ] **Correo y dirección** correctos en `index.html`, `404.html`,
  `privacidad.html` y en los datos estructurados de `index.html`.
- [ ] **Dominio** definido.
- [ ] **Imagen al compartir:** al cambiar de dominio, actualizar `og:url` y
  `og:image` en `index.html` (deben ser URL absolutas).
- [ ] **Licencias de fuentes:** Amsi Pro y Myriad Pro son comerciales; confirmar
  la licencia de webfont.

---

## 2. Opción A — Hosting propio (Apache / cPanel)

1. Entrar al panel del hosting (cPanel, Plesk, etc.) y abrir el **Administrador
   de archivos**.
2. Entrar a la carpeta pública del dominio: normalmente `public_html/`.
3. Subir el archivo **`ruka-kalen-sitio-web.zip`** y descomprimirlo ahí. Debe
   quedar así:

   ```
   public_html/
   ├── index.html
   ├── privacidad.html
   ├── 404.html
   ├── robots.txt
   ├── .htaccess
   └── assets/
   ```

   El sitio debe quedar en la raíz del dominio, no dentro de una subcarpeta.
   Si se publica en una subcarpeta (por ejemplo `dominio.cl/ruka-kalen/`),
   ajustar en `.htaccess` la línea `ErrorDocument 404 /404.html` a
   `ErrorDocument 404 /ruka-kalen/404.html`.

4. Activar **HTTPS/SSL**. En cPanel suele estar en *SSL/TLS Status* con
   Let's Encrypt (gratis y renovación automática).
5. Con HTTPS activo, descomentar en `.htaccess` el bloque de redirección a HTTPS
   (última sección del archivo) para que `http://` lleve a `https://`.
6. Verificar en el navegador: `https://dominio.cl/`.

**Notas**

- `.htaccess` es opcional; el sitio funciona sin él. Agrega tipos MIME
  correctos, compresión, caché y cabeceras de seguridad.
- No hay que crear bases de datos, correos ni tareas programadas.
- No hay PHP, Node, Python ni nada que instalar.

---

## 3. Opción B — GitHub Pages

El repositorio ya está publicado desde la rama `gh-pages`:

- Repositorio: `https://github.com/<cuenta>/ruka-kalen`
- Sitio: `https://<cuenta>.github.io/ruka-kalen/`
- Configuración: *Settings → Pages → Source: Deploy from a branch →
  `gh-pages` / (root)*.

Cada push a `gh-pages` republica el sitio en menos de un minuto. El archivo
`.nojekyll` evita que GitHub procese los archivos con Jekyll.

Para usar un dominio propio en Pages: *Settings → Pages → Custom domain*,
crear el registro DNS que GitHub indique y activar *Enforce HTTPS*.

---

## 4. Dominio y HTTPS

1. En el proveedor del dominio, apuntar el DNS al hosting:
   - **Hosting propio:** registro `A` al IP del servidor (o `CNAME` si el
     proveedor lo indica).
   - **GitHub Pages:** los registros que muestra GitHub en *Custom domain*.
2. Esperar la propagación (puede tardar hasta 24 h, normalmente minutos).
3. Activar el certificado SSL y la redirección a HTTPS.

---

## 5. Verificación después de publicar

- [ ] `https://dominio.cl/` abre la página y se ve correctamente en celular y
  escritorio.
- [ ] El botón **Agenda tu consulta** abre el WhatsApp correcto, con el mensaje
  prellenado.
- [ ] Cada tarjeta de especialidad abre WhatsApp con su mensaje.
- [ ] El enlace **Aviso de privacidad** funciona.
- [ ] Una URL inexistente muestra la página 404 con la marca.
- [ ] El candado de HTTPS aparece y no hay advertencias de contenido mixto.
- [ ] Al compartir el enlace por WhatsApp aparece la tarjeta con la imagen.
- [ ] No hay errores en la consola del navegador.

Comprobaciones rápidas desde una terminal:

```bash
curl -I https://dominio.cl/
curl -I https://dominio.cl/assets/fonts/amsi-pro-regular.woff2
curl -I https://dominio.cl/pagina-que-no-existe
```

Las dos primeras deben responder `200`; la tercera, `404`.

---

## 6. Actualizar el sitio

### Cambiar el número de WhatsApp

1. Reemplazar en **todos** los archivos (principalmente `index.html` y
   `404.html`):

   | Buscar | Reemplazar por |
   |---|---|
   | `56950944500` | número nuevo, sin `+`, sin espacios ni guiones |
   | `+56 9 5094 4500` | número nuevo en formato legible |

2. Verificar que los enlaces queden así:
   `https://wa.me/569XXXXXXXX?text=Hola%2C%20quiero%20agendar...`
3. Republicar (subir por FTP/cPanel o `git push`).

### Cambiar textos, especialidades o dirección

Editar `index.html`. Los textos de cada especialidad están en las tarjetas
`<article class="card">`. La dirección aparece en el hero, en la sección de
contacto y en el pie.

### Actualizar el repositorio

```bash
git add .
git commit -m "descripción del cambio"
git push
```

Si el sitio se publica con GitHub Pages, el push a `gh-pages` basta. Si se
publica en un hosting propio, volver a subir los archivos modificados.

---

## 7. Entrega del repositorio

El repositorio puede transferirse a la cuenta u organización de GitHub del
cliente:

- **Interfaz web:** *Settings → General → Danger Zone → Transfer ownership*.
- **CLI:** `gh api -X POST repos/<cuenta>/ruka-kalen/transfer -f new_owner=<destino>`.

Al transferir:

1. La URL de GitHub Pages cambia a
   `https://<destino>.github.io/ruka-kalen/`.
2. Actualizar `og:url` y `og:image` en `index.html`.
3. Si había dominio propio configurado en Pages, volver a configurarlo.
4. Agregar al equipo de desarrollo como colaborador si se necesita soporte.

El paquete de entrega incluye además un **respaldo del repositorio**
(`ruka-kalen-repositorio.bundle`). Para restaurarlo:

```bash
git clone ruka-kalen-repositorio.bundle ruka-kalen
```

---

## 8. Respaldos

- **Código:** repositorio en GitHub + `ruka-kalen-repositorio.bundle`.
- **Sitio para hosting:** `ruka-kalen-sitio-web.zip`.
- **Contenido:** al ser estático, el respaldo del código es el respaldo del
  sitio.

Recomendación: guardar una copia del ZIP y del bundle fuera del equipo de
desarrollo (nube o disco externo).

---

## 9. Soporte de navegadores

- Chrome, Edge, Firefox y Safari en sus versiones actuales (escritorio y móvil).
- La animación de entrada usa una función moderna de CSS; en navegadores
  antiguos el contenido simplemente se muestra sin animación.
- No requiere JavaScript para funcionar.
