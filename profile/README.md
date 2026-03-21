# Aurora Home

Système de surveillance environnementale connecté — capteurs IoT, dashboard temps réel, firmware ESP32.

---

## Projets

| Dépôt | Description | Stack |
|---|---|---|
| [aurora-home-app](https://github.com/ESP-AuroraHome/aurora-home-app) | Application web — dashboard capteurs, authentification OTP, profil utilisateur | Next.js 15, Prisma, Better Auth |
| [aurora-home-esp32](https://github.com/ESP-AuroraHome/aurora-home-esp32) | Firmware ESP32 — lecture capteurs, publication MQTT via WiFi AP | C++, PlatformIO, MQTT |
| [aurora-home-documentation](https://github.com/ESP-AuroraHome/aurora-home-documentation) | Documentation complète du projet | Next.js 15, Tailwind CSS v4 |

---

## Architecture

```
ESP32 (SCD30 · BME280 · BH1750)
    │  MQTT / WiFi AP
    ▼
Orange Pi  ──  Broker MQTT
    │
    ▼
Next.js App  ──  SSE  ──  Dashboard
    │
  SQLite (Prisma)
```

---

## Capteurs

- **SCD30** — CO₂, température, humidité
- **BME280** — pression atmosphérique, température, humidité
- **BH1750** — luminosité (lux)

---

## Documentation

[aurora-home-documentation](https://github.com/ESP-AuroraHome/aurora-home-documentation)
