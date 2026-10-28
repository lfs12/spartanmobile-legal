# Sitio legal de SpartanMobile — `lfs12.github.io/spartanmobile-legal`

Política de Privacidad y Términos y Condiciones de SpartanMobile (Spartan Tech's C.A.), como sitio
estático para GitHub Pages. Sin dependencias ni build: HTML + CSS.

| URL pública | Archivo |
|---|---|
| https://lfs12.github.io/spartanmobile-legal/ | `index.html` |
| https://lfs12.github.io/spartanmobile-legal/privacidad/ | `privacidad/index.html` |
| https://lfs12.github.io/spartanmobile-legal/terminos/ | `terminos/index.html` |

La app Android usa las dos últimas URLs (`PRIVACY_POLICY_URL` y `TERMS_URL` en
`app/build.gradle.kts`, base `LEGAL_BASE_URL`).

> Estos textos son un borrador técnico basado en lo que hace la app. Haga que un abogado en
> Venezuela los revise.

## 1. Datos de la empresa

Titular: **Spartan Tech's C.A.** (nombre comercial «Grupo Spartan»), RIF J-31399006-0, domicilio fiscal en Calle El Colegio, C.C. Makro, Nivel 1, Oficina 50, Sector Centro, Porlamar, estado Nueva Esparta, Zona Postal 6301. Jurisdicción: estado Nueva Esparta. Contacto de privacidad: aflores@spartantechsorg.com.

Solo queda pendiente `REEMPLAZAR_CODIGO_SEARCH_CONSOLE` (paso 3).

## 2. Publicar (repositorio `lfs12/spartanmobile-legal`)

El repositorio debe ser **público** (GitHub Pages en repos privados requiere plan de pago).
Copie el contenido de esta carpeta a la raíz del repositorio y publique:

```bash
git add .
git commit -m "Actualizar documentos legales"
git push
```

**Settings → Pages:** *Deploy from a branch* → rama `main`, carpeta `/ (root)`. Deje
**Custom domain** vacío y **Enforce HTTPS** activado.

Las rutas son relativas (`../assets/…`), así que funcionan bajo `/spartanmobile-legal/`. Solo
`404.html` usa rutas absolutas con ese prefijo: si cambia el nombre del repositorio,
actualícelas allí y en `canonical`/`og:url`/JSON-LD/`sitemap.xml`.

## 3. Google Search Console

Un sitio en `github.io` no puede verificarse como propiedad de **Dominio** (no controla el DNS de
`github.io`); use una propiedad de **prefijo de URL**:

1. https://search.google.com/search-console → *Agregar propiedad* → **Prefijo de URL** →
   `https://lfs12.github.io/spartanmobile-legal/`.
2. Método **Etiqueta HTML**: copie el valor de `content` y reemplace
   `REEMPLAZAR_CODIGO_SEARCH_CONSOLE` en `index.html`, `privacidad/index.html` y
   `terminos/index.html`. Publique y pulse **Verificar**.
3. En *Sitemaps*, envíe `sitemap.xml`. (No hay `robots.txt`: en un sitio de proyecto los
   buscadores solo leen el de la raíz `lfs12.github.io/robots.txt`.)

### Vínculo con la organización

Los datos estructurados (`application/ld+json`) declaran a **Spartan Tech's C.A.**
(`https://grupospartan.com/#organization`, RIF, domicilio y contactos), el sitio y la app, y cada
documento indica que lo publica esa organización.

Un subdominio de `github.io` pertenece a GitHub, no a la empresa, así que Google no lo trata como
dominio propio de la organización. Si más adelante lo exige una revisión (Google Play, pantalla de
consentimiento OAuth de Google), configure un dominio propio en **Custom domain**, cree el registro
`CNAME` en el DNS de ese dominio hacia `lfs12.github.io`, y actualice `LEGAL_BASE_URL` en la app y
las URLs absolutas del sitio.

## 4. Cambiar los documentos

1. Edite los HTML, actualice la versión y la fecha (`meta`, JSON-LD `dateModified`,
   `sitemap.xml`) y publique.
2. Si el cambio es relevante y quiere que todos los usuarios lo acepten de nuevo, suba
   `LEGAL_TERMS_VERSION` en `app/build.gradle.kts`: la app volverá a mostrar el aviso de
   consentimiento al abrirse.

## Vista previa local

```bash
python -m http.server 8080
```

Abra http://localhost:8080/ (los enlaces canónicos apuntan a la URL publicada; es normal).
