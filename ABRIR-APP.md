# Cómo abrir la app DocuGen

Si la app **no permite abrir** o da errores al ejecutar `npm run dev`, sigue estos pasos.

## 1. Instalación limpia (recomendado)

En PowerShell, dentro de la carpeta del proyecto:

```powershell
cd "c:\Users\ASUS\Downloads\generador-de-facturas-y-cuentas-de-cobro"

# Borrar instalación anterior
Remove-Item -Recurse -Force node_modules -ErrorAction SilentlyContinue
Remove-Item -Force package-lock.json -ErrorAction SilentlyContinue

# Instalar de nuevo
npm install

# Arrancar la app
npm run dev
```

Cuando veas en consola: **`Server running on http://localhost:3000`**, abre el navegador en:

**http://localhost:3000**

---

## 2. Si sigue fallando (Node 24)

Con Node 24 a veces hay conflictos. Prueba con **Node 20 LTS**:

- Instala Node 20 desde https://nodejs.org (versión LTS)
- Vuelve a hacer la instalación limpia del punto 1
- Ejecuta `npm run dev` y abre **http://localhost:3000**

---

## 3. Solo abrir la interfaz (sin login)

Si solo quieres ver la pantalla de la app pero **no podrás iniciar sesión** (no hay backend):

```powershell
npm run dev:ui
```

Luego abre **http://localhost:5173**. Verás la pantalla de login; el inicio de sesión no funcionará hasta que el servidor completo esté en marcha con `npm run dev`.

---

## 4. Cómo compartir la app en otro dispositivo

Con la app en marcha (`npm run dev`), **otros dispositivos en la misma Wi‑Fi** pueden usarla.

### En la misma red (móvil, otra PC, tablet)

1. **Deja el servidor corriendo** en el PC donde ejecutaste `npm run dev`.
2. Al arrancar, la consola muestra algo como:
   ```text
   Server running on http://localhost:3000
   En la red local (otro dispositivo): http://192.168.1.105:3000
   ```
3. En el **otro dispositivo** (móvil, tablet, otro PC):
   - Conéctalo a la **misma red Wi‑Fi** que el PC.
   - Abre el navegador y entra a la URL que salió en la consola, por ejemplo: **http://192.168.1.105:3000** (usa la IP que te muestre tu PC).

### Si no ves la IP en consola

En el **PC donde corre la app**, abre PowerShell y ejecuta:

```powershell
(Get-NetIPAddress -AddressFamily IPv4 | Where-Object { $_.InterfaceAlias -notmatch "Loopback" } | Select-Object -First 1).IPAddress
```

Usa esa IP en el otro dispositivo: **http://ESA_IP:3000** (por ejemplo `http://192.168.1.105:3000`).

### Firewall de Windows

Si desde el otro dispositivo **no carga** la página:

1. Abre **Seguridad de Windows** → **Firewall y protección de red** → **Configuración avanzada**.
2. **Reglas de entrada** → **Nueva regla** → **Puerto** → Siguiente.
3. TCP, puertos específicos: **3000** → Permitir la conexión → Nombre por ejemplo: **DocuGen**.

### Usar la app desde internet (otra red)

Para abrir la app desde fuera de tu casa (por ejemplo el móvil con datos):

- Opción sencilla: usar un **túnel** (por ejemplo [ngrok](https://ngrok.com)) hacia el puerto 3000 de tu PC.
- Opción fija: **subir la app a un hosting** (Vercel, Railway, un VPS, etc.) y acceder por una URL pública.
