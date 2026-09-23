# Gym Tracker — pasos para dejarlo en vivo

Todo lo de esta lista lo tenés que hacer vos: son cosas de tus cuentas
(GitHub, Google, Supabase) o manejo de secretos. Andá en orden; cada valor
está listo para copiar y pegar.

Datos fijos del proyecto:

- Repo: `dannynqn-debug/gym-tracker` (público)
- URL final de la app: `https://dannynqn-debug.github.io/gym-tracker/`
- Proyecto Supabase: `gym-tracker` · ref `hjvituxlaeyyargkynfy`

---

## 1. Subir el código a GitHub

En la Terminal:

```
cd ~/Desktop/gym-tracker && git push -u origin main
```

Si pide usuario y contraseña: el usuario es `dannynqn-debug` y la contraseña
es un token de GitHub (Settings → Developer settings → Personal access tokens
→ Fine-grained → repo `gym-tracker` con permiso Contents: Read and write).

Para comprobar que subió:

```
open https://github.com/dannynqn-debug/gym-tracker
```

## 2. Prender GitHub Pages

1. Entrá a: `https://github.com/dannynqn-debug/gym-tracker/settings/pages`
2. En **Source** elegí **Deploy from a branch**
3. Branch: `main` · carpeta: `/ (root)` → **Save**
4. Esperá 1 o 2 minutos y abrí `https://dannynqn-debug.github.io/gym-tracker/`

Tiene que aparecer la pantalla "Entrar con Google". Todavía no va a
funcionar el login: eso son los pasos 3 y 4.

## 3. Google Cloud (crear el acceso con Gmail)

Entrá a `https://console.cloud.google.com/` y creá un proyecto nuevo llamado:

```
Gym Tracker
```

**3.1 Pantalla de consentimiento** (APIs y servicios → Pantalla de consentimiento de OAuth)

- Tipo de usuario: **Externo**
- Nombre de la app:
  ```
  Gym Tracker
  ```
- Correo de asistencia y correo de contacto: tu Gmail
- Dominio autorizado:
  ```
  supabase.co
  ```
- Permisos (scopes): dejá los básicos (`email`, `profile`, `openid`)
- Al final, **Publicar la app** (estado: En producción). Si queda en Prueba,
  solo entran los mails que cargues a mano.

**3.2 Credenciales** (APIs y servicios → Credenciales → Crear credenciales →
ID de cliente de OAuth → **Aplicación web**)

- Nombre:
  ```
  Gym Tracker web
  ```
- Orígenes de JavaScript autorizados (agregá los dos):
  ```
  https://dannynqn-debug.github.io
  ```
  ```
  http://localhost:8000
  ```
- URI de redireccionamiento autorizado:
  ```
  https://hjvituxlaeyyargkynfy.supabase.co/auth/v1/callback
  ```

Google te va a mostrar un **Client ID** y un **Client Secret**. No me los
pases por chat: van directo a Supabase en el paso siguiente.

## 4. Supabase

Entrá a `https://supabase.com/dashboard/project/hjvituxlaeyyargkynfy`

**4.1 Activar Google**

Authentication → Sign In / Providers → Google:

- Activá el proveedor
- Pegá el **Client ID** y el **Client Secret** del paso 3.2
- Guardá

**4.2 URLs**

Authentication → URL Configuration:

- Site URL:
  ```
  https://dannynqn-debug.github.io/gym-tracker/
  ```
- Redirect URLs (agregá las dos):
  ```
  https://dannynqn-debug.github.io/gym-tracker/
  ```
  ```
  http://localhost:8000/
  ```

## 5. Probar

1. Abrí `https://dannynqn-debug.github.io/gym-tracker/` en el Chrome de tu celular
2. Entrá con Gmail
3. Hacé el onboarding: nombre, rutina y rodilla (**Sí** en tu caso)
4. Completá una serie: se guarda sola y arranca el descanso
5. Menú de Chrome → **Agregar a pantalla de inicio**, para que quede como app

Para que la usen tu hijo y tus amigos, alcanza con pasarles ese link: cada
uno entra con su Gmail y ve solo sus datos.

---

## Para tener en cuenta

- **Supabase gratis se pausa solo** si el proyecto queda sin uso unos días.
  Si un día la app no deja entrar, entrá al dashboard y tocá **Restore**.
- Nunca pongas el Client Secret ni la `service_role key` en el código. En el
  `index.html` solo va la clave pública, que ya está.
- Para cambiar un ejercicio o una rutina se edita el `index.html` y se vuelve
  a pushear: el catálogo vive en el código, no en la base.
