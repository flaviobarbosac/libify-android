# Clampfy — Android (Capacitor)

App Android do Clampfy. O código web fica em `../../frontend/`; este repositório contém o **projeto Gradle/Capacitor**.

## Pré-requisitos

| Ferramenta | Versão |
|------------|--------|
| Node.js | 18+ |
| JDK | 17 ou 21 |
| Android SDK | API 35 + Build-Tools |
| Android Studio | Emulador e debug |

## Setup (Windows)

```powershell
cd C:\Projects\Clampfy\mobile\scripts
.\setup-android-dev.ps1 -PersistUser
.\run-android-dev.ps1 -StartEmulator
```

## Google Sign-In (obrigatório)

1. No [Google Cloud Console](https://console.cloud.google.com/), crie credencial **OAuth Android**:
   - Package: `com.clampfy.app`
   - SHA-1 debug:

```powershell
cd C:\Projects\Clampfy\mobile\scripts
.\get-debug-sha1.ps1
```

2. Mantenha também o **OAuth Web Client** (mesmo ID usado no front) — necessário para validar o token no backend.

## Sincronizar web → Android

```powershell
cd C:\Projects\Clampfy\frontend
npm run cap:sync
npm run cap:open
```

O build Android usa `.env.android` (API dev + `VITE_PLATAFORMA=android`).

## Build debug

```powershell
cd C:\Projects\Clampfy\mobile\android
.\gradlew assembleDebug
```

APK: `app/build/outputs/apk/debug/app-debug.apk`

## Rodar no emulador (recomendado)

AVD padrao: **ClampfyPixel6** (Pixel 6, API 35). Criar uma vez:

```powershell
cd C:\Projects\Clampfy\mobile\scripts
.\setup-android-dev.ps1
sdkmanager "emulator" "system-images;android-35;google_apis_playstore;x86_64"
echo no | avdmanager create avd -n ClampfyPixel6 -k "system-images;android-35;google_apis_playstore;x86_64" -d "pixel_6"
```

Build + instalar + abrir:

```powershell
.\run-android-dev.ps1 -StartEmulator
```

### Troubleshooting emulador (Windows)

| Problema | Solucao |
|----------|---------|
| Emulador fecha sozinho | Preferir **Device Manager** do Android Studio ou `-gpu swiftshader_indirect` |
| `adb` nao encontrado | Rode `setup-android-dev.ps1` e reabra o terminal |
| Tela preta / GPU | Android Studio > AVD > Edit > Graphics: **Software** |
| Login Google falha | Confira SHA-1 debug com `get-debug-sha1.ps1` no Google Cloud |

## Fluxo de telas

O app Android carrega o mesmo front web (Ciclo de Ouro: dashboard, clientes, propostas, cobranças, mais). Login via Google nativo no app; demais telas idênticas ao web dev.
