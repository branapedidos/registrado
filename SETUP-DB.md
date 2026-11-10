# Conectar Vercel + base de datos gratuita (Supabase)

Vercel solo aloja la página; los pedidos se guardan en Supabase (plan gratuito).

## A. Crear la base de datos
1. Entra a https://supabase.com → **Start your project** → inicia sesión con GitHub o correo.
2. **New project**: nombre `brana-pedidos`, crea una contraseña de base de datos (guárdala), elige la región más cercana (por ejemplo *South America (São Paulo)*) y plan **Free**.
3. Espera 1–2 minutos a que el proyecto termine de crearse.
4. Menú izquierdo → **SQL Editor** → **New query**. Pega el contenido de `supabase.sql` y pulsa **Run**. Debe decir *Success*.
5. Menú izquierdo → **Project Settings → API** (o *Connect*). Copia:
   - **Project URL** (`https://xxxx.supabase.co`)
   - **anon / publishable key** (clave pública)

## B. Poner las claves en la app
Abre `config.js` y completa:
```js
window.BRANA_CONFIG = {
  SUPABASE_URL: "https://xxxx.supabase.co",
  SUPABASE_ANON_KEY: "tu-clave-anon-o-publishable"
};
```
Nunca uses la clave `service_role` / secret en este archivo.

## C. Subir a GitHub
Sube a la raíz del repositorio: `index.html`, `config.js`, `.nojekyll`, `README.md` (y opcionalmente `supabase.sql`, `SETUP-DB.md`).

## D. Publicar en Vercel
1. https://vercel.com → inicia sesión con GitHub.
2. **Add New… → Project** → importa tu repositorio.
3. *Framework Preset*: **Other**. Deja *Build Command* y *Output Directory* vacíos.
4. **Deploy**. Vercel te dará una URL `https://tu-proyecto.vercel.app`.
5. Cada vez que hagas *commit* en GitHub, Vercel vuelve a desplegar solo.

## E. Probar
1. Abre la URL de Vercel: abajo de la página debe decir **«Sincronizado con la base de datos ✓»**.
2. Registra un pedido de prueba, ve a Supabase → **Table Editor → pedidos**: debe aparecer la fila.
3. Abre la URL desde otro dispositivo: verás el mismo pedido (se actualiza cada ~15 segundos).

Los pedidos que ya tengas guardados en un navegador se suben solos la primera vez que se conecte.

## Importante (seguridad)
- La app no tiene contraseña: **cualquiera que conozca la URL y la clave pública puede leer y modificar los pedidos**. Es suficiente para uso interno, pero no compartas el enlace públicamente.
- Para protegerla más adelante: activar Supabase Auth, o poner **Vercel Password Protection** (plan de pago) o Cloudflare Access (gratis).
- El plan gratuito de Supabase pausa el proyecto tras 1 semana sin actividad; se reactiva desde su panel.
- Los vouchers (imágenes) se guardan dentro de cada pedido; con muchos vouchers la base crece rápido (límite gratuito 500 MB).

## Si no sincroniza
- Mensaje «No se pudo conectar…»: revisa URL y clave en `config.js`, y que ejecutaste `supabase.sql`.
- Error 401/403: falta la política RLS del paso A4.
- Abre F12 → Consola para ver el error exacto.
