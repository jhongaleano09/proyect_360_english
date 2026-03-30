# Guía de Despliegue en Vercel + Integración en Google Sites

---

## PASO 1 — Preparar los assets

Antes de subir el proyecto, coloca tus archivos en las carpetas indicadas:

```
proyect_360_english/
├── index.html
├── vercel.json
└── assets/
    ├── img/
    │   ├── amazon_360.jpg      ← imagen 360° para "El abrazo de la serpiente"
    │   ├── bogota_360.jpg      ← imagen 360° para "La estrategia del caracol"
    │   └── hotspot.svg         ← ya incluido ✅
    └── audio/
        ├── amazon_jungle.mp3   ← audio ambiente selva
        └── city_bogota.mp3     ← audio ambiente ciudad
```

Ver instrucciones de fuentes gratuitas en:
- `assets/img/README_IMAGES.txt`
- `assets/audio/README_AUDIO.txt`

---

## PASO 2 — Instalar Vercel CLI

```bash
# Requiere Node.js instalado (node.js.org)
npm install -g vercel
```

---

## PASO 3 — Iniciar sesión en Vercel

```bash
vercel login
# Abre el navegador para autenticar con GitHub, Google o email
```

---

## PASO 4 — Desplegar el proyecto

```bash
# Desde la raíz del proyecto
cd proyect_360_english

# Primer despliegue (modo interactivo — acepta las opciones por defecto)
vercel

# Despliegue a producción
vercel --prod
```

Al final del comando verás una URL como:
```
✅ Production: https://colombian-cinema-360.vercel.app
```

---

## PASO 5 — Generar el código QR

### Opción A — Online (rápido)
1. Ve a **qr-code-generator.com** o **qrcodemonkey.com**
2. Pega tu URL de Vercel
3. Elige color dorado (`#F5C518`) sobre fondo negro para coincidir con el diseño
4. Descarga como PNG de al menos 300×300 px

### Opción B — Desde terminal
```bash
# Instalar la herramienta qrcode
npm install -g qrcode

# Generar QR como imagen PNG
qrcode "https://TU-URL.vercel.app" -o qr_colombian_cinema.png
```

---

## PASO 6 — Embeber en Google Sites

Google Sites permite incrustar URLs externas mediante el componente "Embed":

1. Abre tu Google Site y edita la página
2. Clic en **Insert → Embed**
3. En la pestaña **"By URL"**, pega tu URL de Vercel
4. Ajusta el tamaño del iframe: mínimo **480 px de alto** para una buena experiencia
5. Guarda y publica el sitio

> ⚠️ **Importante:** Google Sites aplica un sandbox al iframe que puede bloquear el audio.
> Se recomienda que los estudiantes también puedan abrir la experiencia directamente
> en su navegador móvil escaneando el código QR.

---

## PASO 7 — Actualizaciones futuras

```bash
# Cada vez que modifiques el código o los assets:
vercel --prod
```

---

## NOTAS DE RENDIMIENTO MÓVIL

| Recurso | Recomendación | Razón |
|---|---|---|
| Imagen 360° | JPG, máx 4 MB c/u | Reduce tiempo de carga en datos móviles |
| Audio | MP3 128 kbps, máx 3 MB | Compatible con todos los navegadores móviles |
| Hotspot SVG | Ya optimizado ✅ | SVG es vectorial, pesa < 2 KB |
| Conexión | WiFi o 4G recomendado | 360° + audio = ~10 MB total |
