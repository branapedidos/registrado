# Registro de pedidos – Brana

Aplicación web de una sola página (HTML + JavaScript) para registrar y dar seguimiento a pedidos
(Shalom, Olva, retiro en tienda y delivery en Lima). **No requiere contraseña ni servidor.**

## Archivos
- `index.html` – la aplicación completa
- `.nojekyll` – evita que GitHub Pages procese el sitio con Jekyll
- `config.js` – claves de la base de datos (opcional)
- `supabase.sql` y `SETUP-DB.md` – conexión con Supabase
- `README.md` – estas instrucciones

## Publicar en GitHub Pages
1. Crea un repositorio nuevo en GitHub (por ejemplo `registro-pedidos`).
2. Sube `index.html`, `.nojekyll` y `README.md` a la raíz del repositorio.
3. Ve a **Settings → Pages**.
4. En **Source** elige **Deploy from a branch**, rama `main`, carpeta `/ (root)` y pulsa **Save**.
5. Espera 1–2 minutos: tu app quedará en `https://TU-USUARIO.github.io/registro-pedidos/`.

## Probar en tu computadora
Haz doble clic en `index.html`, o ejecuta `python3 -m http.server 8000` en esta carpeta
y abre `http://localhost:8000`.

## Notas
- Los pedidos se guardan en el **navegador** (localStorage) de cada dispositivo. Para respaldar o
  compartir, usa **Descargar Excel**.
- Requiere internet solo para cargar la fuente Inter y la librería de Excel (xlsx-js-style, CDN).
- La copia automática a Google Sheets solo funciona dentro de Claude; en GitHub se omite sin errores.
