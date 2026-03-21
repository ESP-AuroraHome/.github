<div align="center">

<img src="https://raw.githubusercontent.com/ESP-AuroraHome/aurora-home-documentation/main/public/assets/logo.png" width="72" height="72" alt="Aurora Home" />

# Aurora Home

**Système de surveillance environnementale connecté**

Capteurs IoT · Dashboard temps réel · Firmware ESP32 · Authentification OTP

<br/>

[![Next.js](https://img.shields.io/badge/Next.js_15-000000?style=for-the-badge&logo=nextdotjs&logoColor=white)](https://nextjs.org)
[![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white)](https://www.typescriptlang.org)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS_v4-06B6D4?style=for-the-badge&logo=tailwindcss&logoColor=white)](https://tailwindcss.com)
[![C++](https://img.shields.io/badge/C++-00599C?style=for-the-badge&logo=cplusplus&logoColor=white)](https://isocpp.org)
[![PlatformIO](https://img.shields.io/badge/PlatformIO-F5822A?style=for-the-badge&logo=platformio&logoColor=white)](https://platformio.org)
[![MQTT](https://img.shields.io/badge/MQTT-660066?style=for-the-badge&logo=mqtt&logoColor=white)](https://mqtt.org)

</div>

---

## Vue d'ensemble

Aurora Home est un système embarqué de surveillance environnementale. Un ESP32 collecte en continu des données de capteurs (CO₂, température, humidité, pression, luminosité) et les publie via MQTT. Une application Next.js reçoit ces données, les stocke et les affiche dans un dashboard en temps réel via Server-Sent Events.

```
┌─────────────────────────────────────────────────────────────────┐
│                                                                 │
│   ESP32                                                         │
│   ├── SCD30    CO₂ · Température · Humidité                    │
│   ├── BME280   Pression · Température · Humidité               │
│   └── BH1750   Luminosité                                       │
│         │                                                       │
│         │  MQTT (WiFi AP)                                       │
│         ▼                                                       │
│   Orange Pi ── Broker MQTT                                      │
│         │                                                       │
│         │  instrumentation.ts                                   │
│         ▼                                                       │
│   Next.js App ── SSE ──► Dashboard                             │
│         └── SQLite (Prisma)                                     │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## Dépôts

### [`aurora-home-app`](https://github.com/ESP-AuroraHome/aurora-home-app)
Application web complète — dashboard capteurs, graphiques interactifs, authentification OTP sans mot de passe, profil utilisateur, support PWA.

> Next.js 15 · Prisma · SQLite · Better Auth · Recharts · Tailwind CSS v4

---

### [`aurora-home-esp32`](https://github.com/ESP-AuroraHome/aurora-home-esp32)
Firmware ESP32 — initialisation des capteurs I²C, lecture périodique, fusion des données, publication MQTT en JSON.

> C++ · PlatformIO · Arduino framework · ArduinoJson · PubSubClient

---

### [`aurora-home-documentation`](https://github.com/ESP-AuroraHome/aurora-home-documentation)
Documentation complète du projet — guide utilisateur, référence technique, API, conventions de code et guide de contribution.

> Next.js 15 · Tailwind CSS v4 · Déployé en statique

---

## Capteurs & Montages

Tous les capteurs communiquent via le bus **I²C** sur les broches `GPIO21 (SDA)` et `GPIO22 (SCL)` de l'ESP32.

Broches I²C de l'ESP32 : `GPIO21 (SDA)` · `GPIO22 (SCL)` · alimentation `3.3V`

---

### SCD30 — CO₂ · Température · Humidité

![Montage SCD30](images/wiring-scd30.png)

| Broche SCD30 | ESP32 | Note |
|---|---|---|
| VDD | 3.3V | |
| GND | GND | |
| SDA | GPIO21 | |
| SCL | GPIO22 | |
| SEL | GND | Force le mode I²C |

---

### BME280 — Pression · Température · Humidité

![Montage BME280](images/wiring-bme280.png)

| Broche BME280 | ESP32 | Note |
|---|---|---|
| VCC | 3.3V | |
| GND | GND | |
| SDA | GPIO21 | |
| SCL | GPIO22 | |
| CSB | 3.3V | Force le mode I²C |
| SDO | GND | Adresse `0x76` · 3.3V → `0x77` |

---

### BH1750 — Luminosité

![Montage BH1750](images/wiring-bh1750.png)

| Broche BH1750 | ESP32 | Note |
|---|---|---|
| VCC | 3.3V | |
| GND | GND | |
| SDA | GPIO21 | |
| SCL | GPIO22 | |
| ADDR | GND | Adresse `0x23` · 3.3V → `0x5C` |

---

## Contribuer

Les contributions sont les bienvenues sur chacun des dépôts indépendamment.
Consulter le [guide de contribution](https://github.com/ESP-AuroraHome/aurora-home-documentation) pour le workflow complet (fork → branch → PR).

---

<div align="center">

Epitech Rennes · Promo 2026

</div>
