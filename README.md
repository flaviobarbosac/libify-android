# Libify — Android (Capacitor)

App Android do Libify. O código web fica em `../../frontend/`; este repositório contém o **projeto Gradle/Capacitor**.

## Pré-requisitos

| Ferramenta | Versão |
|------------|--------|
| Node.js | 18+ |
| JDK | 17 ou 21 |
| Android SDK | API 35 + Build-Tools |
| Android Studio | Emulador e debug |

## Setup (Windows)

```powershell
cd C:\Projects\Libify\mobile\scripts
.\setup-android-dev.ps1 -PersistUser
```

## Google Sign-In (obrigatório)

1. No [Google Cloud Console](https://console.cloud.google.com/), crie credencial **OAuth Android**:
   - Package: `com.libify.app`
   - SHA-1 debug:

```powershell
cd C:\Projects\Libify\mobile\scripts
.\get-debug-sha1.ps1
```

2. Mantenha também o **OAuth Web Client** (mesmo ID usado no front) — necessário para validar o token no backend.

## Sincronizar web → Android

```powershell
cd C:\Projects\Libify\frontend
npm run cap:sync
npm run cap:open
```

O build Android usa `.env.android` (API dev + `VITE_PLATAFORMA=android`).

## Build debug

```powershell
cd C:\Projects\Libify\mobile\android
.\gradlew assembleDebug
```

APK: `app/build/outputs/apk/debug/app-debug.apk`

## Fluxo de telas

O app Android carrega o mesmo front web (Ciclo de Ouro: dashboard, clientes, propostas, cobranças, mais). Login via Google nativo no app; demais telas idênticas ao web dev.
