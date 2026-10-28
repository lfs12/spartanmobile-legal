# Sitio legal de SpartanMobile — `legal.grupospartan.com`

Política de Privacidad y Términos y Condiciones de SpartanMobile (Spartan Tech's C.A.), como sitio
estático para GitHub Pages. Sin dependencias ni build: HTML + CSS.

| URL pública | Archivo |
|---|---|
| https://legal.grupospartan.com/ | `index.html` |
| https://legal.grupospartan.com/privacidad/ | `privacidad/index.html` |
| https://legal.grupospartan.com/terminos/ | `terminos/index.html` |

La app Android usa las dos últimas URLs (`PRIVACY_POLICY_URL` y `TERMS_URL` en
`app/build.gradle.kts`).

> Estos textos son un borrador técnico basado en lo que hace la app. **Antes de publicarlos,
> haga que un abogado en Venezuela los revise.**

## 1. Datos de la empresa

Titular: **Spartan Tech's C.A.** (nombre comercial «Grupo Spartan»), RIF J-31399006-0, domicilio fiscal en Calle El Colegio, C.C. Makro, Nivel 1, Oficina 50, Sector Centro, Porlamar, estado Nueva Esparta, Zona Postal 6301. Jurisdicción: estado Nueva Esparta. Contacto de privacidad: aflores@spartantechsorg.com.

Solo queda pendiente `REEMPLAZAR_CODIGO_SEARCH_CONSOLE` (código de verificación, paso 4), o quitar
esas líneas si verifica el dominio por DNS.

## 2. Publicar en GitHub Pages

Se recomienda un repositorio **público** propio para el sitio (GitHub Pages en repos privados
requiere plan de pago), por ejemplo `grupospartan/spartanmobile-legal`:

```bash
cd legal-site
git init -b main
git add .
git commit -m "Sitio legal de SpartanMobile"
git remote add origin https://github.com/<organizacion>/spartanmobile-legal.git
git push -u origin main
```

En GitHub: **Settings → Pages**

1. **Source:** *Deploy from a branch* → rama `main`, carpeta `/ (root)` → **Save**.
2. **Custom domain:** `legal.grupospartan.com` → **Save** (el archivo `CNAME` ya lo contiene).
3. Cuando el DNS propague, marque **Enforce HTTPS**.

## 3. DNS de `grupospartan.com`

En el proveedor DNS del dominio, cree:

| Tipo | Nombre | Valor |
|---|---|---|
| `CNAME` | `legal` | `<organizacion>.github.io` |

Recomendado: en **GitHub → Settings de la organización → Pages → Add a domain**, verifique
`grupospartan.com` (GitHub le dará un registro `TXT`). Eso impide que otra cuenta de GitHub
tome el subdominio.

Comprobar: `nslookup legal.grupospartan.com` debe resolver a GitHub y la página debe abrir con
HTTPS.

## 4. Vincular el dominio con la organización en Google

1. **Google Search Console** (https://search.google.com/search-console) → *Agregar propiedad*.
   - Recomendado: propiedad de **Dominio** `grupospartan.com` verificada con registro `TXT`
     en el DNS (cubre todos los subdominios). En ese caso puede quitar las líneas
     `google-site-verification` de los HTML.
   - Alternativa: propiedad de **prefijo de URL** `https://legal.grupospartan.com/` con
     *Etiqueta HTML*: copie el `content` y reemplace `REEMPLAZAR_CODIGO_SEARCH_CONSOLE` en los
     tres HTML.
2. En Search Console → *Sitemaps*, envíe `https://legal.grupospartan.com/sitemap.xml`.
3. Los datos estructurados (`application/ld+json`) de `index.html` declaran la organización
   (`https://grupospartan.com/#organization`), el sitio y la app, y cada documento indica que lo
   publica esa organización. Si `grupospartan.com` publica también un bloque `Organization`,
   use el mismo `@id` para que Google los relacione.
4. Si más adelante se publica en Google Play o se usa OAuth de Google, use estas mismas URLs
   como política de privacidad y términos: deben estar en un dominio verificado de la
   organización, que es lo que se logra con los pasos anteriores.

## 5. Cambiar los documentos

1. Edite los HTML, actualice la versión y la fecha (`meta`, JSON-LD `dateModified`,
   `sitemap.xml`) y publique.
2. Si el cambio es relevante y quiere que todos los usuarios lo acepten de nuevo, suba
   `LEGAL_TERMS_VERSION` en `app/build.gradle.kts`: la app volverá a mostrar el aviso de
   consentimiento al abrirse.

## Vista previa local

```bash
cd legal-site
python -m http.server 8080
```

Abra http://localhost:8080/.
