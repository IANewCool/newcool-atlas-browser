# Backlog - NewCool Atlas Browser

## Prioridad Alta

### 1. Auto-detección de plataforma en página de descarga
**Estado:** Pendiente
**Dependencia:** Builds completados para todas las plataformas

**Descripción:**
Implementar detección automática del sistema operativo y arquitectura del usuario para recomendar la versión correcta del navegador.

**Requisitos:**
- [ ] Detectar OS: Windows, macOS, Linux, Android
- [ ] Detectar arquitectura: x64, ARM64, ARM32
- [ ] Detectar Apple Silicon vs Intel en macOS
- [ ] Mostrar botón de descarga recomendado prominente
- [ ] Ofrecer "Otras plataformas" como opción secundaria

**Implementación propuesta:**
```javascript
function detectPlatform() {
  const ua = navigator.userAgent;
  const platform = navigator.platform;

  // Android
  if (/Android/i.test(ua)) {
    return /arm64|aarch64/i.test(ua) ? 'android-arm64' : 'android-arm32';
  }

  // macOS
  if (/Mac/i.test(platform)) {
    // Detectar Apple Silicon
    const isAppleSilicon = async () => {
      try {
        const canvas = document.createElement('canvas');
        const gl = canvas.getContext('webgl');
        const renderer = gl.getParameter(gl.RENDERER);
        return /Apple M/i.test(renderer);
      } catch { return false; }
    };
    return isAppleSilicon() ? 'macos-arm64' : 'macos-x64';
  }

  // Windows
  if (/Win/i.test(platform)) return 'windows-x64';

  // Linux
  if (/Linux/i.test(platform) && !/Android/i.test(ua)) return 'linux-x64';

  return 'unknown';
}
```

**URLs de descarga:**
| Plataforma | Archivo | URL |
|------------|---------|-----|
| macOS x64 | NewCool-Atlas-145.0.7560-x64.dmg | TBD |
| macOS ARM64 | NewCool-Atlas-145.0.7560-arm64.dmg | TBD |
| Windows x64 | NewCool-Atlas-145.0.7560-win64.zip | TBD |
| Linux x64 | NewCool-Atlas-145.0.7560-linux-x64.tar.gz | TBD |
| Android ARM64 | NewCool-Atlas-145.0.7560-arm64.apk | TBD |
| Android ARM32 | NewCool-Atlas-145.0.7560-arm32.apk | TBD |

---

## Prioridad Media

### 2. GitHub Releases automáticos
**Estado:** Pendiente

**Descripción:**
Cuando un build termine exitosamente, crear automáticamente un GitHub Release con los artifacts.

**Requisitos:**
- [ ] Workflow que detecte build exitoso
- [ ] Crear release con tag de versión
- [ ] Subir artifacts (DMG, ZIP, APK, tar.gz)
- [ ] Generar changelog automático

---

### 3. Caching de compilación (ccache/sccache)
**Estado:** Pendiente

**Descripción:**
Implementar cache de objetos compilados para acelerar builds subsecuentes.

**Beneficio:** Reducir tiempo de build de ~4h a ~1h

---

### 4. Notificaciones de build
**Estado:** Pendiente

**Descripción:**
Webhook para notificar cuando builds terminen (éxito o fallo).

**Opciones:**
- Discord webhook
- Slack webhook
- Email

---

## Prioridad Baja

### 5. Self-hosted runners
**Estado:** Pendiente

**Descripción:**
Configurar servidor Vultr como runner de GitHub Actions para mantener cache entre builds.

---

### 6. Firma de código
**Estado:** Pendiente

**Descripción:**
- macOS: Notarización con Apple Developer
- Windows: Firma con certificado EV
- Android: Firma con keystore propio

---

## Completados

- [x] Workflow para macOS x64 (Intel)
- [x] Workflow para macOS ARM64 (Apple Silicon)
- [x] Workflow para Windows x64
- [x] Workflow para Linux x64
- [x] Workflow para Android ARM32
- [x] Build manual en Vultr para Android ARM64

---

*Última actualización: 2026-01-05*
