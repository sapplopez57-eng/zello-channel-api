# 🎤 Zello Web PTT - Aplicación Web Push-to-Talk

Aplicación web lista para usar que permite comunicarse con canales de Zello directamente desde el navegador, **sin necesidad de backend, tokens especiales o configuraciones complejas**.

## ✨ Características

- **Sin dependencias de backend**: Funciona completamente en el navegador
- **Sin tokens obligatorios**: Usa usuario y contraseña directamente
- **Interfaz moderna**: Diseño atractivo y responsive
- **Push-to-Talk**: Botón grande para transmitir voz
- **Multi-dispositivo**: Funciona en desktop y móvil (touch)
- **Configuración guardada**: Recuerda tus datos (excepto contraseña)
- **Estado en tiempo real**: Indicadores visuales de conexión y transmisión
- **Log de eventos**: Mensajes informativos de todas las acciones

## 🚀 Cómo Usar

### Opción 1: Abrir Directamente (Recomendado para pruebas)

1. **Descarga el archivo HTML**:
   - El archivo `zello-web-ptt.html` está listo para usar
   - No necesitas instalar nada

2. **Ábrelo en tu navegador**:
   - Haz doble clic en el archivo
   - O arrástralo a una pestaña del navegador

3. **Importante para acceso al micrófono**:
   - ⚠️ **Los navegadores requieren HTTPS para acceder al micrófono**
   - Si abres el archivo localmente (`file://`), algunos navegadores pueden bloquear el micrófono
   - Soluciones:
     - Usa un servidor local con HTTPS (ver abajo)
     - O usa Chrome que es más permisivo con archivos locales
     - O sube el archivo a un hosting con HTTPS (GitHub Pages, Netlify, etc.)

### Opción 2: Servidor Local con HTTPS

#### Usando Python (fácil):

```bash
# Instalar mkcert para certificados locales
# macOS:
brew install mkcert nss
mkcert -install
mkcert localhost 127.0.0.1

# Windows (con Chocolatey):
choco install mkcert
mkcert -install
mkcert localhost 127.0.0.1

# Linux:
sudo apt install libnss3-tools
mkcert -install
mkcert localhost 127.0.0.1

# Luego sirve el archivo con HTTPS:
cd sdks/js/examples
python3 -m http.server --ssl-key localhost.key --ssl-cert localhost.crt 8000
```

#### Usando Node.js:

```bash
# Instalar serve globalmente
npm install -g serve

# Generar certificados (si no los tienes)
openssl req -x509 -newkey rsa:4096 -keyout localhost.key -out localhost.crt -days 365 -nodes -subj "/CN=localhost"

# Servir con HTTPS
serve --ssl-cert localhost.crt --ssl-key localhost.key -p 8000
```

#### Usando el webpack dev server incluido:

```bash
cd sdks/js
npm install
npm run build
npm run dev
```

## 📋 Configuración Necesaria

### Datos que necesitas:

1. **Nombre de la Red Zello**: El nombre de tu red en Zello Work
   - Ejemplo: `mi-empresa`, `taxi-central`, etc.

2. **Canal**: El nombre del canal al que quieres unirte
   - Ejemplo: `CANAL1`, `DESPACHO`, `GENERAL`

3. **Usuario y Contraseña** O **Auth Token**:
   - **Opción A (Recomendada)**: Usuario y contraseña de un usuario del canal
   - **Opción B**: Auth token desde Zello Work Console (opcional)

### ¿Dónde obtener estos datos?

1. **Si ya tienes una red Zello Work**:
   - Ve a [Zello Work Console](https://zellowork.io/console)
   - Inicia sesión
   - Tu nombre de red está en la URL o en la configuración
   - Los canales están en la sección "Channels"
   - Los usuarios están en la sección "Users"

2. **Si no tienes una red**:
   - Crea una cuenta gratuita en [zellowork.io](https://zellowork.io)
   - Sigue el asistente de configuración
   - Crea un canal y usuarios

## 🎯 Uso Paso a Paso

1. **Abrir la aplicación** en tu navegador

2. **Completar el formulario**:
   ```
   Nombre de la Red Zello: tu-red-zello
   Canal: CANAL1
   Usuario: usuario1
   Contraseña: ********
   Auth Token: (déjalo vacío si usas usuario/contraseña)
   ```

3. **Marcar "Recordar configuración"** (opcional)
   - Guarda red, canal y usuario
   - NO guarda contraseña por seguridad

4. **Hacer clic en "Conectar a Zello"**

5. **Esperar conexión**:
   - Verás mensajes de estado
   - Cuando diga "Conectado", el botón PTT se activará

6. **Presiona y mantén el botón PTT** para hablar:
   - Mantén presionado mientras hablas
   - Suelta para dejar de transmitir
   - En móvil: toca y mantén

7. **Escuchar mensajes entrantes**:
   - Los mensajes de voz se reproducen automáticamente
   - Verás notificaciones en el log

## 🔧 Solución de Problemas

### El micrófono no funciona

**Problema**: El navegador bloquea el acceso al micrófono

**Soluciones**:
1. **Usa HTTPS**: Los navegadores requieren HTTPS para `getUserMedia`
   - Sube el archivo a GitHub Pages, Netlify, Vercel (todos con HTTPS gratis)
   - O usa un servidor local con HTTPS (ver arriba)

2. **Permisos del navegador**:
   - Haz clic en el ícono de candado en la barra de direcciones
   - Permite el acceso al micrófono
   - Recarga la página

3. **Chrome permite archivos locales**:
   - Chrome es más permisivo con `file://`
   - Prueba abrir directamente el archivo HTML

### Error de conexión

**Problema**: No puede conectar a Zello

**Verifica**:
1. ✅ Nombre de red correcto (sensible a mayúsculas/minúsculas)
2. ✅ Canal existe y está activo
3. ✅ Usuario y contraseña correctos
4. ✅ Tienes conexión a internet (requerido aunque sea local)
5. ✅ El canal no está lleno o deshabilitado

### Se desconecta frecuentemente

**Causas posibles**:
- Mala conexión a internet
- El servidor Zello está caído
- Token expirado (si usas authToken)

**Soluciones**:
- La app intenta reconectar automáticamente
- Revisa tu conexión a internet
- Verifica el estado de Zello Work

## 🌐 Despliegue en Internet

### GitHub Pages (Gratis)

1. Crea un repositorio en GitHub
2. Sube el archivo `zello-web-ptt.html`
3. Renómbralo a `index.html`
4. Ve a Settings > Pages
5. Activa GitHub Pages
6. ¡Listo! Tendrás una URL HTTPS

### Netlify (Gratis)

1. Arrastra el archivo HTML a [Netlify Drop](https://app.netlify.com/drop)
2. Obtendrás una URL HTTPS instantáneamente

### Vercel (Gratis)

1. Instala Vercel CLI: `npm i -g vercel`
2. Ejecuta `vercel` en la carpeta
3. Sigue las instrucciones

### Tu propio servidor

1. Sube el archivo HTML a tu servidor web
2. Asegúrate de tener HTTPS configurado
3. Accede desde cualquier dispositivo

## 📱 Uso en Móvil

La aplicación es completamente responsive y funciona en:

- **iOS Safari** (iOS 12+)
- **Android Chrome** (Android 6+)
- **Cualquier navegador moderno**

**En móvil**:
- El botón PTT responde al touch
- Mantiene la transmisión mientras mantengas presionado
- Funciona en segundo plano (la voz sigue transmitiendo)

## 🔒 Seguridad

### ¿Es seguro usar usuario y contraseña?

- **Sí**, la conexión es encriptada (WSS - WebSocket Seguro)
- Las credenciales viajan encriptadas a los servidores de Zello
- No se almacenan en ningún servidor intermedio
- La opción "Recordar configuración" NO guarda la contraseña

### Mejores prácticas:

1. ✅ Usa HTTPS siempre
2. ✅ No compartas tu archivo HTML con credenciales guardadas
3. ✅ Usa contraseñas fuertes
4. ✅ Revoca usuarios comprometidos desde Zello Work Console

## 🛠️ Personalización

### Cambiar colores

Edita las variables CSS en el `<style>`:

```css
/* Color de fondo */
body {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
}

/* Color del botón PTT */
.ptt-button {
    background: linear-gradient(145deg, #ff6b6b, #ee5a5a);
}
```

### Cambiar tamaño del botón

```css
.ptt-button {
    width: 200px;  /* Cambia este valor */
    height: 200px; /* Cambia este valor */
}
```

### Agregar más canales

Puedes modificar el código para permitir seleccionar entre múltiples canales:

```javascript
// Agrega un selector en el HTML
<select id="channelSelect">
    <option value="CANAL1">Canal 1</option>
    <option value="CANAL2">Canal 2</option>
</select>
```

## 📊 Eventos que Monitorea

La aplicación muestra en el log:

- ✅ Conexión iniciada
- ✅ Conexión exitosa
- ✅ Mensajes de voz entrantes
- ✅ Mensajes de texto entrantes
- ✅ Estado del canal (usuarios en línea)
- ✅ Transmisión iniciada/finalizada
- ✅ Errores y desconexiones
- ✅ Reconexión automática

## 🔄 Actualizaciones

El SDK se carga desde CDN automáticamente:

```html
<script src="https://cdn.jsdelivr.net/npm/zello-channel-api@latest/sdks/js/zello-channel-sdk.js"></script>
```

Para usar una versión específica:

```html
<script src="https://cdn.jsdelivr.net/npm/zello-channel-api@1.2.3/sdks/js/zello-channel-sdk.js"></script>
```

## 💡 Tips y Trucos

1. **Prueba primero en desktop**: Más fácil para depurar
2. **Usa auriculares**: Evita feedback/audio loop
3. **Verifica el volumen**: Ajusta volumen del sistema y navegador
4. **Mantén la pestaña activa**: Algunos navegadores pausan scripts en segundo plano
5. **Compartir URL**: Una vez desplegado, comparte la URL con tu equipo

## ❓ FAQ

### ¿Necesito internet?

**Sí**. Aunque la app es local, se conecta a los servidores de Zello en internet.

### ¿Funciona sin authToken?

**Sí**. Puedes usar usuario y contraseña directamente.

### ¿Puedo usarlo en mi red WiFi local?

**Sí**, pero necesitas:
- Acceso a internet (para conectar a Zello)
- HTTPS (para el micrófono)
- Un dispositivo que sirva la página (puede ser cualquier PC/laptop)

### ¿Cuántos usuarios pueden conectarse?

Depende de tu plan de Zello Work:
- **Gratis**: Hasta 100 usuarios
- **Pago**: Según tu plan

### ¿Se puede usar como intercomunicador?

**Sí**. Es perfecto para:
- Despacho de taxis
- Equipos de seguridad
- Coordinación de eventos
- Comunicación en almacenes
- Cualquier escenario push-to-talk

## 📞 Soporte

Si tienes problemas:

1. Revisa esta documentación
2. Verifica tus credenciales de Zello
3. Prueba en otro navegador
4. Revisa la consola del navegador (F12) para errores

## 📄 Licencia

Este ejemplo usa el SDK oficial de Zello Channel API. Revisa la licencia del repositorio principal para términos de uso.

---

**¡Listo! Ahora tienes una aplicación web de comunicación push-to-talk funcionando en minutos, sin backend ni configuraciones complejas.** 🎉
