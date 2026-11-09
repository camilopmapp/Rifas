# App de Rifas — instalación (una sola vez, ~20 min)

Archivos:
- `index.html` → la aplicación completa.
- `firestore.rules` → reglas de seguridad de la base de datos.

## 1. Crear el proyecto en Firebase
1. Entra a https://console.firebase.google.com → **Agregar proyecto** (por ejemplo `rifas-amigos`). Google Analytics: desactivado.
2. **Authentication** → Comenzar → **Google** → Habilitar → Guardar.
3. **Firestore Database** → Crear base de datos → **modo producción** → ubicación `southamerica-east1 (São Paulo)`.
4. Firestore → pestaña **Reglas** → borra lo que hay, pega todo `firestore.rules` → **Publicar**.

## 2. Conectar la app
1. ⚙️ Configuración del proyecto → **Tus apps** → ícono web `</>` → registra la app (no marques Hosting).
2. Copia el bloque `firebaseConfig` y pégalo en `index.html`, en la sección marcada **"1. PEGA AQUÍ…"**.

> La `apiKey` de Firebase no es secreta: la seguridad está en las reglas.

## 3. Hacerte administrador
Firestore → **Datos** → **Iniciar colección**:
- ID de colección: `organizadores`
- ID del documento: **tu correo de Google en minúsculas** (ej. `camilo@gmail.com`)
- Campos: `nombre` (string) = tu nombre · `admin` (boolean) = `true`

## 4. Publicar en GitHub Pages
1. Crea un repositorio (ej. `rifas`) y sube `index.html`.
2. Settings → **Pages** → Branch `main` / `root` → Save.
3. Tu link queda así: `https://TU-USUARIO.github.io/rifas/`
4. En Firebase → Authentication → **Configuración** → **Dominios autorizados** → agrega `TU-USUARIO.github.io`.

## 5. Uso
**Organizador**
1. Abre el link en Chrome o Safari (no dentro de WhatsApp: ahí falla el inicio de sesión con Google) → **Entrar con Google**.
2. **+ Nueva rifa** → llena la configuración → **Guardar cambios** → **Abrir ventas**.
3. **Compartir** → copia el link o envíalo por WhatsApp.
4. Cuando llegue un comprobante y veas el dinero en tu cuenta → **Confirmar pago**. Si alguien no paga → **Liberar**.
5. Antes del sorteo → **Cerrar ventas** → escribe el número de la lotería → **Publicar resultado**.

**Agregar amigos organizadores:** en *Mis rifas*, sección *Organizadores autorizados* (solo la ve el administrador), escribe su correo de Gmail.
Cada amigo ve y administra **solo sus propias rifas**.

**Participante:** abre el link, toca sus números, escribe nombre y celular, paga y envía el comprobante con el botón de WhatsApp. Su boleta se actualiza sola cuando el organizador confirma.

## Cómo funciona (resumen)
- Un número apartado queda ocupado hasta que el organizador lo confirma o lo libera. No vence solo.
- El público solo ve "ocupado". Nombre y celular solo los ve el organizador.
- Dos personas no pueden apartar el mismo número al mismo tiempo (transacción en la base de datos).
- Si el número ganador no se vendió, el premio queda para el organizador.
- Exportar CSV abre en Excel con la lista de compradores.

## Límites del plan gratuito (Spark)
50.000 lecturas y 20.000 escrituras al día: alcanza de sobra para varias rifas simultáneas entre amigos. No hay costo mientras no actives el plan de pago.
