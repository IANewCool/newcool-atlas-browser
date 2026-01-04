<p align="center">
  <img src="https://avatars.githubusercontent.com/u/126275955?v=4" width="120" alt="NewCool Planet">
</p>

<h1 align="center">NewCool Atlas Browser</h1>

<p align="center">
  Navegador web basado en Chromium, optimizado para el ecosistema educativo NewCool.
</p>

## Características

- **Homepage**: planet.newcool.io
- **Branding**: NewCool Atlas
- **Basado en**: Chromium 145.0.7560
- **Plataformas**: macOS, Android, Windows, Linux

## Descargas

Visita [Releases](https://github.com/IANewCool/newcool-atlas-browser/releases) para descargar la última versión.

| Plataforma | Arquitectura | Formato |
|------------|--------------|---------|
| macOS | x64, arm64 | .dmg |
| Android | arm64 | .apk |
| Windows | x64 | .exe (próximamente) |
| Linux | x64 | .deb (próximamente) |

## Build Manual

### Requisitos

- macOS 13+ / Ubuntu 22.04+
- 100GB+ espacio en disco
- 16GB+ RAM
- Xcode (macOS) / build-essential (Linux)

### Pasos

```bash
# 1. Clonar depot_tools
git clone https://chromium.googlesource.com/chromium/tools/depot_tools.git
export PATH="$PWD/depot_tools:$PATH"

# 2. Obtener Chromium
mkdir chromium && cd chromium
fetch --nohooks chromium
cd src
gclient runhooks

# 3. Aplicar patches de NewCool
git apply /path/to/patches/*.patch

# 4. Configurar build
gn gen out/Default --args='is_debug=false is_official_build=true'

# 5. Compilar
autoninja -C out/Default chrome
```

## GitHub Actions

Este repositorio usa GitHub Actions para builds automáticos:

- **build-android.yml**: Genera APK para Android
- **build-macos.yml**: Genera DMG para macOS

Para ejecutar un build manual:
1. Ve a Actions → Workflow
2. Click "Run workflow"
3. Selecciona opciones y ejecuta

## Estructura

```
newcool-atlas-browser/
├── patches/                    # Patches de personalización
│   ├── 0001-homepage.patch
│   ├── 0002-newtab.patch
│   └── 0003-branding.patch
├── .github/workflows/          # GitHub Actions
│   ├── build-android.yml
│   └── build-macos.yml
└── README.md
```

## Licencia

- Chromium: BSD License
- NewCool Branding: © NewCool 2026

## Links

- [NewCool Planet](https://planet.newcool.io)
- [NewCool API](https://api.newcool.io)
- [Documentación](https://docs.newcool.io)
