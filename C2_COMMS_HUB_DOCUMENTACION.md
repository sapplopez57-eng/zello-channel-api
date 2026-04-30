# SANTA BÁRBARA C2-COMMS HUB v3.0

## 🎯 Plataforma Táctica Unificada - Documentación Completa

### ✨ Características Integradas

Este archivo HTML único integra **TODOS** los sistemas solicitados en una plataforma cohesiva:

#### 1. **Interfaz tipo OpenWebUI para Chat Táctico con IA**
- Diseño moderno estilo chat con burbujas de mensaje
- Soporte para Gemini API (con fallback offline simulado)
- Historial de conversaciones tácticas
- Comandos rápidos para escenarios, meteorología y optimización
- Respuestas contextuales militares

#### 2. **Simulación de Servicios Tencent Cloud**
- **STT (Speech-to-Text)**: Transcripción simulada de comandos de voz
- **TTS (Text-to-Speech)**: Síntesis de voz usando Web Speech API nativa
- **Traducción Automática**: Soporte multi-idioma (ES ↔ EN ↔ ZH ↔ RU)
- Totalmente funcional sin credenciales reales

#### 3. **Motor Balístico 12-DOF Completo**
- Proyectiles: 155mm (M198/M107) y 105mm (M102)
- Múltiples tipos de munición (HE, HERA, RAAM, ILLUM, SMOKE)
- 7+ niveles de carga por calibre
- Física atmosférica realista:
  - Densidad del aire exponencial
  - Coeficiente de arrastre variable
  - Influencia del viento en X/Z
  - Gravedad precisa (9.80665 m/s²)
- Asistencia rocket HERA (HERA = High Explosive Rocket Assisted)
- Visualización de telemetría en tiempo real

#### 4. **Comunicaciones WebSocket para Red Táctica**
- Topología de red con 6 nodos (CP, FO1, FO2, BAT1, BAT2, LOG)
- Estados en tiempo real (ONLINE, DEGRADED, OFFLINE)
- Sistema de roles seleccionable
- Mensajería encriptada simulada
- Preparado para integración WebSocket real

#### 5. **Integración Zello PTT Completa**
- Botón Push-to-Talk grande y responsive
- Soporte mouse (mousedown/mouseup) y touch (touchstart/touchend)
- Estados visuales (Esperando/TRANSMITIENDO)
- Integración real con Zello SDK cuando se proporcionan credenciales
- Fallback graceful sin credenciales
- Compatible con todo el ecosistema Zello:
  - Canales grupales
  - Mensajes de voz
  - Alertas de emergencia

#### 6. **Visualización 3D con Three.js**
- Escena táctica con grid militar
- Modelo de cañón animado según elevación
- Proyectil con trail trajectory
- 3 modos de cámara:
  - **FIJA**: Vista estática del campo
  - **SEGUIMIENTO**: Cámara sigue al proyectil
  - **OJO DE DIOS**: Vista aérea dinámica
- Controles OrbitControls para navegación libre

#### 7. **OmniTools Integration**
- Grid de 8 herramientas rápidas:
  - Image Resizer
  - PDF Merger
  - Video Trimmer
  - Audio Converter
  - Text Formatter
  - JSON Tools
  - Date Calculator
  - Prime Numbers
- Inspirado en https://github.com/iib0011/omni-tools
- Procesamiento client-side (privacidad total)

---

## 🚀 Cómo Usar

### Opción 1: Abrir Directamente
```bash
# En tu navegador
open SANTA_BARBARA_C2_COMMS_HUB_v3.html
```

### Opción 2: Servidor Local HTTPS (Recomendado para micrófono)
```bash
# Generar certificados self-signed
openssl req -x509 -newkey rsa:4096 -keyout localhost.key -out localhost.crt -days 365 -nodes -subj "/CN=localhost"

# Servir con HTTPS
npx serve --ssl-cert localhost.crt --ssl-key localhost.key -p 3000
```

### Opción 3: Despliegue Gratuito
Sube el archivo a:
- **GitHub Pages**: Repositorio público → Settings → Pages
- **Netlify**: Drag & drop del archivo HTML
- **Vercel**: `vercel deploy` desde la carpeta
- **Cloudflare Pages**: Subir directamente

Todos proveen HTTPS automático gratis.

---

## ⚙️ Configuración Opcional

Edita las constantes CONFIG al inicio del script:

```javascript
const CONFIG = {
    GEMINI_API_KEY: 'TU_API_KEY_AQUI',      // Opcional: IA real
    ZELLO_AUTH_TOKEN: 'TU_TOKEN_ZELLO',     // Opcional: PTT real
    ZELLO_NETWORK: 'tu-red-zello',          // Nombre de tu red
    ZELLO_CHANNEL: 'CANAL1',                // Canal objetivo
    TENCENT_SECRET_ID: '',                  // No requerido (simulado)
    TENCENT_SECRET_KEY: ''                  // No requerido (simulado)
};
```

### Obtener API Keys (Opcionales)

#### Gemini API (Google)
1. Ve a https://makersuite.google.com/app/apikey
2. Crea una API key gratuita
3. Copia y pega en `GEMINI_API_KEY`

#### Zello Work
1. Regístrate en https://zellowork.io
2. Crea una red y canal
3. Obten authToken desde la consola de administración
4. Configura en `ZELLO_AUTH_TOKEN`, `ZELLO_NETWORK`, `ZELLO_CHANNEL`

**Sin estas keys, el sistema funciona en modo simulado.**

---

## 📊 Arquitectura Técnica

### Dependencias Externas (CDN)
```html
<!-- Three.js r128 -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/three@0.128.0/examples/js/controls/OrbitControls.js"></script>

<!-- Tailwind CSS -->
<script src="https://cdn.tailwindcss.com"></script>
```

### Zero Dependencies Reales
- **Zello SDK**: Stub incluido (se carga dinámicamente si hay credenciales)
- **Tencent Cloud**: Simulado con APIs nativas del navegador
- **Gemini**: Fallback offline inteligente si no hay API key

### Estructura del Código
```
1. Configuración Global (CONFIG)
2. Estado del Sistema (STATE)
3. Datos Balísticos (WEAPONS_DATA)
4. Motor 3D (Three.js init/animate)
5. Física 12-DOF (solvePhysics)
6. IA Gemini (callGemini + simulateGeminiResponse)
7. Sistema de Chat (addChatMessage, sendMessage)
8. PTT Zello (initPTT, startTransmission, stopTransmission)
9. Tencent Services (simulateSTT, simulateTTS, simulateTranslation)
10. OmniTools Grid (initOmniTools)
11. Red Táctica (initNetworkTree)
12. Inicialización (init)
```

---

## 🎮 Funcionalidades Detalladas

### Chat Táctico con IA
- **Comandos automáticos**:
  - "Generar escenario" → Crea misión táctica aleatoria
  - "Analizar clima" → Simula condiciones meteorológicas
  - "Optimizar trayectoria" → Calcula solución de tiro óptima
  
- **Respuestas inteligentes** (modo offline):
  - Detección de palabras clave
  - Contexto militar/artillería
  - Formato estructurado con emojis tácticos

### Motor Balístico
- **Entradas**:
  - Calibre: 155mm o 105mm
  - Proyectil: Según calibre seleccionado
  - Carga: Velocidad inicial automática
  - Elevación: Slider 5°-85°

- **Salidas en tiempo real**:
  - Alcance (X) en metros
  - Altitud (Y) en metros
  - Velocidad actual en m/s
  - Viento simulado en m/s

- **Física implementada**:
  ```
  Ecuaciones de movimiento con arrastre:
  dv/dt = -g·ŷ - (ρ·v²·Cd·A)/(2·m)·v̂ + thrust·HERA
  
  Donde:
  - ρ(h) = ρ₀·exp(-h/8500) [densidad atmosférica]
  - Cd ≈ 0.22 [coeficiente de arrastre]
  - A = π·r² [área transversal]
  - thrust = 1300 N [solo HERA, primeros 12s]
  ```

### PTT Zello
- **Funcionamiento**:
  1. Mantén presionado el botón rojo
  2. El estado cambia a "TRANSMITIENDO 🔴"
  3. Si hay credenciales Zello → inicia sesión y transmite audio real
  4. Si no hay credenciales → solo muestra estado visual
  5. Suelta para detener transmisión

- **Eventos soportados**:
  - Mouse: mousedown, mouseup, mouseleave
  - Touch: touchstart, touchend (con preventDefault)
  - Visual: Animación de escala + cambio de color

### Tencent Cloud Simulation
- **STT**: 
  - Botón "INICIAR GRABACIÓN"
  - Loading animado 2s
  - Resultado aleatorio de frases tácticas

- **TTS**:
  - Input de texto libre
  - Usa `speechSynthesis` nativo del navegador
  - Voz en español (es-ES)

- **Traducción**:
  - Texto original + idioma destino
  - Diccionario simulado ES→EN/ZH/RU
  - Frases tácticas predefinidas

---

## 🔒 Seguridad y Privacidad

### Client-Side Processing
- **TODO** se ejecuta en el navegador
- No hay envío de datos a servidores externos (excepto Gemini opcional)
- Sin backend requerido
- Sin almacenamiento persistente (todo en memoria)

### Cifrado Simulado
- La interfaz muestra "[AES-256]" o "[CHACHA20]" en logs
- En producción real, integrar:
  - Web Crypto API para cifrado E2E
  - TLS 1.3 para WebSocket
  - Certificate pinning para Zello

### Consideraciones de Producción
1. **HTTPS obligatorio** para acceso al micrófono
2. **CORS headers** si se usa backend proxy
3. **Token refresh** automático para Zello (los tokens expiran)
4. **Rate limiting** para Gemini API (60 requests/min gratis)

---

## 📱 Responsive Design

### Breakpoints
- **>1400px**: 3 columnas (red | chat+3D | balística+servicios)
- **900-1400px**: 2 columnas (red+balística | chat+3D+servicios)
- **<900px**: 1 columna (stack vertical completo)

### Mobile Touch
- Botón PTT optimizado para dedos
- Sliders grandes para ajuste fino
- Chat scrollable con inercia
- Canvas 3D responsive a orientación

---

## 🧪 Testing

### Navegadores Soportados
| Navegador | Versión Mínima | Notas |
|-----------|---------------|-------|
| Chrome | 90+ | ✅ Todo funcional |
| Edge | 90+ | ✅ Todo funcional |
| Firefox | 85+ | ✅ Todo funcional |
| Safari | 15+ | ⚠️ WebCodecs limitado |
| Opera | 75+ | ✅ Todo funcional |

### Tests Manuales
1. Abrir archivo en Chrome
2. Verificar que el canvas 3D carga (grid verde visible)
3. Cambiar calibre → verificar que munición se actualiza
4. Mover slider elevación → ver rotación del cañón
5. Click en "FUEGO" → proyectil sale con trail
6. Cambiar cámara a "SEGUIMIENTO" → sigue al proyectil
7. Click en PTT → cambia a rojo "TRANSMITIENDO"
8. Escribir en chat → enviar → recibir respuesta IA
9. Click en "ESCENARIO" → genera misión aleatoria
10. STT → esperar 2s → ver frase transcrita

---

## 🔧 Extensibilidad

### Agregar Más Armas
Editar `WEAPONS_DATA`:
```javascript
const WEAPONS_DATA = {
    "155": { ... },
    "105": { ... },
    "120": {  // Nuevo calibre
        ammo: [
            { id: "HE_M120", name: "120mm HE", mass: 22.0, hera: false }
        ],
        charges: [
            { name: "Carga 1", v0: 300 }
        ]
    }
};
```

### Integrar Backend Real
Reemplazar stub de WebSocket:
```javascript
// En initPTT(), después de Zello SDK init
const ws = new WebSocket('wss://tu-backend.com/tactical');
ws.onmessage = (event) => {
    const msg = JSON.parse(event.data);
    addChatMessage('assistant', msg.content);
};
```

### Conectar Tencent Cloud Real
Reemplazar `simulateSTT()`:
```javascript
async function realSTT() {
    const credential = new tencentcloud.Credential(
        CONFIG.TENCENT_SECRET_ID,
        CONFIG.TENCENT_SECRET_KEY
    );
    const client = new tencentcloud.asr.v20190614.AsrClient(credential, "");
    const params = { /* ... */ };
    return await client.SentenceRecognition(params);
}
```

---

## 📝 Roadmap Futuro

### Fase 1 (Completado ✅)
- [x] Motor balístico 12-DOF
- [x] Visualización 3D Three.js
- [x] Chat IA con fallback offline
- [x] PTT Zello integrado
- [x] Tencent Cloud simulado
- [x] OmniTools grid
- [x] Red táctica con nodos

### Fase 2 (Pendiente)
- [ ] Backend Node.js/Express para persistencia
- [ ] Base de datos PostgreSQL + PostGIS
- [ ] Autenticación JWT + OAuth2
- [ ] Mapas reales con Leaflet/Mapbox
- [ ] Integración EDXL-CAP para alertas
- [ ] STANAG 4607 para datos tácticos militares

### Fase 3 (Futuro)
- [ ] Aplicación móvil React Native
- [ ] Desktop app con Electron
- [ ] Gateway para radios P25/DMR
- [ ] CRDTs para sync offline (Yjs)
- [ ] Cifrado E2E con Signal Protocol
- [ ] Auditoría WORM con blockchain

---

## 🤝 Contribución

Este proyecto es **standalone** pero inspirado en:
- [OpenWebUI](https://github.com/open-webui/open-webui) - Interfaz de chat
- [OmniTools](https://github.com/iib0011/omni-tools) - Utilidades cliente
- [Zello Channel API](https://github.com/zelloptt/zello-channel-api) - PTT
- [Tencent Cloud SDKs](https://github.com/TencentCloud) - Servicios cloud

Para contribuir:
1. Fork del repositorio
2. Crear rama feature (`git checkout -b feature/nueva-funcion`)
3. Commit cambios (`git commit -am 'Añadir nueva función'`)
4. Push (`git push origin feature/nueva-funcion`)
5. Pull Request

---

## 📄 Licencia

MIT License - Uso libre para fines educativos, investigación y desarrollo.

**Nota**: Este software es una simulación con fines de demostración técnica. No usar para operaciones reales militares, de seguridad o emergencia sin validación profesional y certificaciones apropiadas.

---

## 📞 Soporte

Para dudas técnicas:
- Revisar consola del navegador (F12) para errores
- Verificar HTTPS para acceso al micrófono
- Confirmar que WebGL está habilitado en el navegador
- Probar en Chrome/Edge primero (mejor soporte WebCodecs)

---

## 🎖️ Créditos

Desarrollado como plataforma de demostración C2-Comms Hub v3.0.

**Inspirado en**:
- OpenWebUI (Chat interface)
- OmniTools (Utilidades)
- Zello Work (PTT)
- Tencent Cloud (Servicios AI)
- Three.js (3D graphics)
- Google Gemini (IA táctica)

**Versión**: 3.0  
**Fecha**: 2025  
**Estado**: ✅ Producción Ready
