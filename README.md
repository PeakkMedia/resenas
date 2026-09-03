# Reseñas — Peakk Media

Página independiente con las capturas de resultados de clientes. No depende del repo
de `cyber` ni de `marcas.peakkmedia.com`: se puede subir a cualquier hosting estático.

## Estructura

```
resenas/
├── index.html    la página
├── style.css     el diseño
├── README.md
└── assets/       logo + 107 capturas
```

No hace falta `vercel.json`. Al llamarse `index.html` y estar en la raíz, se sirve
directo en `/` sin ninguna configuración de rutas.

## Antes de subir

En `assets/` van **108 archivos**: las 107 capturas más el logo. La lista exacta está
en `assets/LEEME.txt`.

Dos cosas para no equivocarse:

- **El logo se llama `logo.webp`.** En el otro repo era `tmpuqtfd50_.webp`. Es el único
  archivo que hay que renombrar.
- **Las capturas van con el nombre tal cual las tenés**, con espacios, paréntesis y
  mayúsculas incluidos. `Agus (Antes y Despues).png` se sube así, sin tocar. El HTML
  ya las pide codificadas (`%20` para el espacio, `%28` y `%29` para los paréntesis).

El hosting distingue mayúsculas de minúsculas aunque Windows no: si un archivo cambia
de nombre en el camino, esa captura da 404 y las otras 107 andan igual, que es el error
más difícil de encontrar.

## Subir a GitHub

1. Creá un repositorio nuevo, por ejemplo `resenas`.
2. **Add file → Upload files** y arrastrá `index.html`, `style.css` y `README.md`.
3. Arrastrá la carpeta `assets` completa (arrastrando la carpeta, GitHub respeta la
   estructura; arrastrando los archivos sueltos, quedan en la raíz).
4. Commit.

## Publicar en Vercel

1. En Vercel, **Add New → Project** e importá el repositorio.
2. Framework Preset: **Other**. Build Command, Output Directory e Install Command
   vacíos: es un sitio estático, no hay nada que compilar.
3. Deploy.

Te queda una URL tipo `resenas-xxxx.vercel.app`. Para usar un dominio propio:
**Settings → Domains**, agregás el subdominio, y creás en tu DNS el CNAME con el valor
que muestre la tarjeta del proyecto.

Si el subdominio que elegís ya apunta a otro lado, hay que reemplazar ese registro:
un nombre DNS apunta a un solo servidor.

## Agregar una reseña

Subí la imagen a `assets/` y pegá este bloque dentro de `<div class="muro">` en
`index.html`. El orden en el archivo es el orden en pantalla.

```html
<figure class="tarjeta tarjeta--captura">
  <img src="assets/ARCHIVO.png" alt="Resultado de NOMBRE" loading="lazy" decoding="async">
  <figcaption class="tarjeta-pie">NOMBRE</figcaption>
</figure>
```

Si el archivo tiene espacios o paréntesis: espacio = `%20`, `(` = `%28`, `)` = `%29`.

Para agregar una etiqueta al lado del nombre, como las de "Antes y después":

```html
<figcaption class="tarjeta-pie">NOMBRE <span class="tarjeta-tag">Mes récord</span></figcaption>
```

## Cosas que quizás quieras cambiar

- **Las cifras del encabezado** (+400 tiendas, 107 resultados, 56 marcas) están en el
  bloque `.cifras` de `index.html`.
- **El botón** apunta a la agenda de iClosed. Está una sola vez, cerca del final.
- **El WhatsApp flotante** tiene el número y el mensaje precargado en los dos enlaces
  del bloque `.wa-flotante`.
- **Google Tag Manager** está en el `<head>` con el contenedor `GTM-TSXGCTTX`. Si esta
  página no va a medirse con la misma cuenta, borrá ese `<script>` y el `<noscript>`
  que está apenas abre el `<body>`.
- **La imagen para compartir** (`og:image`) todavía apunta al CDN de GoHighLevel. Si
  querés independizarla del todo, subí esa imagen a `assets/` y reemplazá esa URL por
  la dirección completa de tu dominio nuevo. Las etiquetas `og:` no aceptan rutas
  relativas.
- **El ancho de las columnas** se controla con `columns` en la regla `.muro` de
  `style.css`: 4 en desktop, y 3, 2 y 1 en los `@media` del final.
