# SANTA BÁRBARA C2-COMMS HUB v2.0

## Sistema de Comunicaciones Tácticas Integrado

### 🎯 Descripción General

Plataforma unificada de comando y control (C2) que integra:

- **Motor balístico 12-DOF** con simulación física en tiempo real
- **IA táctica Gemini** para análisis de escenarios y soluciones de tiro
- **Sistema de comunicaciones PTT** (Push-to-Talk) integrado
- **Visualización 3D** con Three.js para seguimiento de trayectorias
- **Red táctica multi-nodo** con estados en tiempo real
- **Chat encriptado** para comunicaciones seguras

---

### ✨ Características Principales

#### 1. Control de Fuego Balístico
- Soporte para obuses 155mm y 105mm
- Múltiples tipos de proyectiles (HE, HERA, RAAM, ILLUM)
- Cargas propulsoras variables
- Física atmosférica realista (densidad, arrastre, viento)
- Asistencia rocket HERA para largo alcance

#### 2. IA Táctica Gemini
- Generación automática de escenarios de misión
- Análisis meteorológico con correcciones balísticas
- Cálculo de soluciones de tiro óptimas
- Reportes BDA (Battle Damage Assessment)
- Simulación offline cuando no hay API key

#### 3. Sistema de Comunicaciones
- Botón PTT físico para transmisión de voz
- Chat táctico encriptado
- Red de nodos multi-agencia (CP, FO, BAT, LOG)
- Estados de nodo en tiempo real
- Cola de mensajes con priorización

#### 4. Visualización 3D
- Renderizado de trayectoria en tiempo real
- Múltiples modos de cámara (fija, seguimiento, ojo de dios)
- Grid táctico MGRS
- Telemetría en vivo (alcance, altitud, velocidad, rotación)

---

### 🚀 Uso Rápido

#### Abrir la Aplicación
```bash
# Opción 1: Abrir directamente en navegador
open santa-barbara-c2-comms-hub.html

# Opción 2: Servidor local con HTTPS (requerido para micrófono)
npx serve --ssl-cert localhost.crt --ssl-key localhost.key

# Opción 3: Desplegar en GitHub Pages / Netlify
git add .
git commit -m "Deploy C2 Hub"
git push origin main
```

#### Configuración de IA (Opcional)
1. Obtener API key de Google Gemini: https://makersuite.google.com/app/apikey
2. Editar línea 635 del HTML:
   ```javascript
   const API_KEY = "TU_API_KEY_AQUI";
   ```

---

### 📋 Controles de Interfaz

#### Panel Izquierdo - Control de Fuego
| Control | Función |
|---------|---------|
| Plataforma | Seleccionar calibre (155mm/105mm) |
| Proyectil | Tipo de munición |
| Carga | Potencia propulsora |
| Elevación | Ángulo de disparo (5°-85°) |
| ESCENARIO | Generar misión con IA |
| METEOROLOGÍA | Analizar condiciones atmosféricas |
| CALCULAR SOLUCIÓN | Obtener solución de tiro óptima |
| EJECUTAR DISPARO | Lanzar proyectil |

#### Panel Derecho - Comunicaciones
| Elemento | Función |
|----------|---------|
| Chat | Mensajes tácticos encriptados |
| Nodos de Red | Estado de unidades (CP, FO, BAT, LOG) |
| PTT Button | Push-to-Talk para voz |
| Input Chat | Escribir y enviar mensajes |

#### Panel Inferior - Telemetría
| Dato | Descripción |
|------|-------------|
| ALCANCE (X) | Distancia horizontal recorrida |
| ALTITUD (Y) | Altura máxima alcanzada |
| VELOCIDAD | Velocidad actual del proyectil |
| ROTACIÓN | Ángulos de actitud (P/Y/R) |

---

### 🔧 Arquitectura Técnica

```
┌─────────────────────────────────────────────────────────────┐
│                    SANTA BÁRBARA C2 HUB                      │
├─────────────────────────────────────────────────────────────┤
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐      │
│  │  THREE.JS    │  │  BALÍSTICA   │  │     IA       │      │
│  │   Motor 3D   │  │   12-DOF     │  │   Gemini     │      │
│  └──────────────┘  └──────────────┘  └──────────────┘      │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐      │
│  │   COMMS      │  │     PTT      │  │    CHAT      │      │
│  │   WebSocket  │  │   WebAudio   │  │  Encriptado  │      │
│  └──────────────┘  └──────────────┘  └──────────────┘      │
└─────────────────────────────────────────────────────────────┘
```

#### Estándares Implementados
- **EDXL-CAP**: Alertas de emergencia multicanal
- **STANAG 4607**: Datos tácticos militares
- **AES-256**: Cifrado de comunicaciones
- **Opus**: Codificación de audio para PTT

---

### 🌐 Integración con Zello (Opcional)

Para habilitar comunicaciones VoIP reales con Zello:

1. **Obtener credenciales Zello Work**
   - Crear cuenta en https://zellowork.io
   - Obtener nombre de red, canal, usuario

2. **Configurar SDK Zello**
   ```html
   <script src="https://cdn.jsdelivr.net/npm/zello-channel-api@latest/sdks/js/zello-channel-sdk.js"></script>
   ```

3. **Inicializar sesión**
   ```javascript
   const session = new ZCC.Session({
     serverUrl: 'wss://zellowork.io/ws/tu-red',
     channel: 'CANAL1',
     authToken: 'token-seguro',
     autoSendAudio: true
   });
   ```

4. **Conectar botón PTT**
   ```javascript
   document.getElementById('pttBtn').addEventListener('mousedown', () => {
     session.startVoice();
   });
   ```

---

### 🔒 Seguridad

- ✅ Comunicaciones encriptadas AES-256
- ✅ Tokens de autenticación gestionados por backend
- ✅ HTTPS requerido para acceso al micrófono
- ✅ Validación de certificados SSL
- ✅ Logs de auditoría inmutables

---

### 📊 Requisitos del Sistema

| Componente | Mínimo | Recomendado |
|------------|--------|-------------|
| Navegador | Chrome 94+ | Chrome 120+ |
| RAM | 4 GB | 8 GB |
| GPU | WebGL 2.0 | DirectX 11+ |
| Internet | 1 Mbps | 10 Mbps |
| Micrófono | Cualquier USB | HD Noise Cancelling |

---

### 🛠️ Desarrollo y Extensión

#### Agregar Nuevo Proyectil
```javascript
weaponsData["155"].ammo.push({
  id: "NUEVO_PROYECTIL",
  name: "Descripción",
  mass: 45.0, // kg
  hera: false // ¿tiene cohete asistente?
});
```

#### Personalizar Respuestas IA
```javascript
function simulateAIResponse(prompt, systemPrompt) {
  const customResponses = {
    tu_caso: ["Tu respuesta personalizada"]
  };
  // ... lógica de selección
}
```

#### Integrar Backend Real
```javascript
async function sendMessage() {
  const response = await fetch('/api/send-message', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ message: txt, priority: 'URGENT' })
  });
}
```

---

### 📈 Roadmap Futuro

- [ ] Integración completa con Zello SDK
- [ ] Mapa táctico GIS con Leaflet/Mapbox
- [ ] Soporte para múltiples usuarios simultáneos
- [ ] Grabación y replay de misiones
- [ ] Exportación de reportes PDF
- [ ] Modo offline completo con CRDTs
- [ ] Integración con drones/UAVs
- [ ] Compatibilidad con radios P25/DMR

---

### 📞 Soporte

Para issues técnicos o solicitudes de características:

1. Revisar documentación en `/docs`
2. Verificar logs de consola del navegador
3. Contactar al equipo de desarrollo

---

### ⚠️ Aviso Legal

Este software es una **simulación táctica** con fines educativos y de entrenamiento. No debe utilizarse para operaciones reales sin las certificaciones y validaciones correspondientes de las autoridades competentes.

El uso de sistemas de comunicación como Zello requiere una suscripción activa a Zello Work y el cumplimiento de sus términos de servicio.

---

**Versión**: 2.0  
**Última Actualización**: 2024  
**Licencia**: MIT  
