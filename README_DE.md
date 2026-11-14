# BTC Calc Card – Bitcoin- & Sats-Rechner

[![hacs_badge](https://img.shields.io/badge/HACS-Custom-41BDF5.svg)](https://github.com/hacs/integration) [![GitHub total downloads](https://img.shields.io/github/downloads/jinx-22/btc-calc-card/total?style=flat-square&color=red)](https://github.com/jinx-22/btc-calc-card/releases/) [![GitHub release](https://img.shields.io/github/release/jinx-22/btc-calc-card?include_prereleases=&sort=semver&color=blue)](https://github.com/jinx-22/btc-calc-card/releases/) [![File size](https://img.shields.io/github/size/jinx-22/btc-calc-card/btc-calc-card.js?label=Card%20Size)](https://github.com/jinx-22/btc-calc-card) [![last commit](https://img.shields.io/github/last-commit/jinx-22/btc-calc-card)](https://github.com/jinx-22/btc-calc-card/commits/main) [![stars](https://img.shields.io/github/stars/jinx-22/btc-calc-card)](https://github.com/jinx-22/btc-calc-card/stargazers) [![Donate Bitcoin](https://img.shields.io/badge/%E2%82%BF-Bitcoin-F7931A?style=flat-square)](#bitcoin) [![Donate Lightning](https://img.shields.io/badge/%E2%9A%A1-Lightning-FFD700?style=flat-square)](#lightning)

🇬🇧 [**English**](https://github.com/jinx-22/btc-calc-card/blob/main/README.md) · 🇩🇪 **Deutsch**

---

**BTC Calc Card** ist eine Home-Assistant-Karte, die mit deinen eigenen Preis-Sensoren zwischen Bitcoin, Sats und beliebig vielen Währungen umrechnet – und den Spread eines Bitcoin-Angebots berechnet.

**Aktuelle Version: 0.4.6**

Den Verlauf findest du im [CHANGELOG](CHANGELOG.md).

Screenshot mit 4 Währungen und aktiviertem Spread-Rechner:
<br>
<img width="40%" height="auto" alt="preview-de" src="images/preview-de.png" />

---

> **Hinweis:** Lade das Dashboard nach dem Update mit `Strg + F5` hart neu und leere den Browser-Cache, damit Editor und Karte die neue Version laden.

---

## 📖 Über BTC Calc Card

Gib in einem beliebigen Feld einen Betrag ein, und alle anderen Felder werden sofort berechnet: wie viele Sats du für 100 € bekommst, was 10.000 Sats in Euro, Dollar usw. kosten. Die aktuellen Preise stehen oben in der Karte. Optional berechnet die Karte auch den **Spread** eines Angebots, zum Beispiel beim Kauf von Bitcoin mit Aufschlag.

### Highlights

- Beliebig viele Währungen – ein Preis-Sensor pro Währung, im Editor hinzugefügt
- Nur aktive Währungen werden angezeigt und berechnet, die Reihenfolge ist frei änderbar
- Live-Umrechnung in beide Richtungen zwischen Sats / BTC und jeder Währung
- Das Bitcoin-Feld lässt sich zwischen **Sats** und **BTC** umschalten
- Aktueller Preis pro Währung oben, mit dem Wert von 1 Einheit in Sats
- Optionaler **Angebotsrechner**: Spread eines Angebots prüfen oder die Sats bei einem Aufschlag bzw. Nachlass berechnen
- Aufschlag / Nachlass in **%**, **Sats** oder **BTC**
- Merkt sich deine Eingaben im Browser
- Responsives Layout, auch für die App (Preis-Kacheln zu zweit nebeneinander)
- Live-Vorschau im Karten-Picker
- Visueller Home-Assistant-Editor
- Deutsch und Englisch (folgt der HA-Sprache)

---

# 📦 Installation

## Einfache Installation → [In HACS öffnen](https://my.home-assistant.io/redirect/hacs_repository/?owner=jinx-22&repository=btc-calc-card&category=plugin)

## HACS Marketplace -> bald verfügbar!

1. **HACS** öffnen
2. **Frontend** auswählen
3. Nach **BTC Calc Card** suchen
4. Karte installieren
5. Home Assistant oder den Browser neu laden

## Manuell

1. `btc-calc-card.js` herunterladen
2. Nach `/config/www/community/btc-calc-card/` kopieren
3. Unter **Einstellungen → Dashboards → Ressourcen** folgende Ressource hinzufügen:

   `/local/community/btc-calc-card/btc-calc-card.js`

   Typ: **JavaScript-Modul**

Danach den Browser neu laden, z. B. mit **Strg + F5**.

---

# ⚙️ Beispielkonfiguration

```yaml
type: custom:btc-calc-card
title: Bitcoin Rechner
show_spread: true
currencies:
  - entity: sensor.bitcoin_price_eur
    code: EUR
    symbol: €
  - entity: sensor.bitcoin_price_usd
    code: USD
    symbol: $
  - entity: sensor.bitcoin_price_gbp
    code: GBP
    symbol: £
    active: false
```

Die Sensoren müssen den **Preis von 1 BTC** in der jeweiligen Währung als Zahl liefern. Alle nicht aufgeführten Optionen verwenden ihren Standardwert.

---

# 📋 Konfigurationsoptionen

| Option        | Standard                                  | Typ     | Beschreibung |
|---------------|-------------------------------------------|---------|--------------|
| `type`        | `custom:btc-calc-card`                    | string  | Kartentyp |
| `title`       | `Bitcoin Rechner` / `Bitcoin Calculator`  | string  | Kartentitel (abhängig von der HA-Sprache). Ein leerer String blendet den Titel aus |
| `show_spread` | `false`                                   | boolean | Angebotsrechner unter den Feldern anzeigen |
| `currencies`  | –                                         | Liste   | Ein Eintrag pro Währung (siehe unten). Die Reihenfolge der Liste ist die Reihenfolge in der Karte |

### Währungseinträge (`currencies`)

| Option   | Standard             | Typ     | Beschreibung |
|----------|----------------------|---------|--------------|
| `entity` | –                    | string  | Sensor mit dem Preis von 1 BTC (`sensor`, `input_number` oder `number`) |
| `code`   | Einheit des Sensors  | string  | Kurzkürzel über dem Preis und als Feldname, z. B. `EUR` |
| `symbol` | `code`               | string  | Symbol hinter dem Betrag, z. B. `€` |
| `active` | `true`               | boolean | Diese Währung anzeigen und berechnen. Inaktive Währungen bleiben in der Konfiguration |

Ohne Entität zeigt die Karte Demowerte, bis du im Editor deine Sensoren auswählst. Ist ein Sensor nicht verfügbar, zeigt die Karte für diese Währung „nicht verfügbar“ und sperrt das zugehörige Feld.

Wenn du die Karte aus dem Karten-Picker hinzufügst, sucht sie selbst nach passenden Sensoren (Entitäts-ID oder Name enthält „btc“ oder „bitcoin“, Zahl als Zustand, Einheit EUR, USD, GBP, CHF oder JPY).

---

# 🧮 Rechner

- **Bitcoin-Feld:** Betrag in Sats oder BTC (Umschaltung im Feld). Darunter zeigt die Karte die jeweils andere Einheit.
- **Währungsfelder:** ein Feld pro aktiver Währung. Eine Eingabe in einem beliebigen Feld füllt alle anderen.
- Ein als Dezimalzeichen getippter Punkt wird automatisch zum Dezimalzeichen deiner Sprache.

---

# 💱 Angebotsrechner

Aktivierung mit `show_spread: true` (oder im Editor). Oben rechts wählst du die Währung, dazu einen von zwei Modi. **Es müssen immer beide Werte eingegeben werden.**

### Spread prüfen

Gib die **Menge** ein, die du erhältst (Sats oder BTC), und den **Kaufbetrag**. Die Karte zeigt, wie viel mehr (oder weniger) als den Marktpreis du zahlst.

### Sats berechnen

Gib den **Kaufbetrag** und den **Aufschlag / Nachlass** in %, Sats oder BTC ein (negativ = Nachlass). Die Karte zeigt die Sats, die du erhältst.

### Ergebnisse

Beide Modi zeigen dieselben Ergebnisse in derselben Reihenfolge:

| Ergebnis | Bedeutung |
|----------|-----------|
| Aufschlag / Abschlag in % | `Angebotspreis / Marktpreis - 1` |
| Aufschlag / Abschlag in Währung | Kaufbetrag minus Marktwert der erhaltenen Sats |
| Aufschlag / Abschlag in Sats | Sats zum Marktpreis minus erhaltene Sats |
| Du erhältst | Menge in Sats, darunter der BTC-Wert |
| Sats zum Marktpreis | was der Kaufbetrag zum aktuellen Marktpreis ergäbe |
| Angebotspreis | `Kaufbetrag / Menge in BTC` |
| Marktpreis | aktueller Preis von 1 BTC aus deinem Sensor |

---

# 📸 Screenshot

Screenshot mit 4 Währungen und aktiviertem Spread-Rechner:
<br>
<img width="40%" height="auto" alt="preview-de" src="images/preview-de.png" />

Der Screenshot zeigt Beispielpreise.

---

# 🐛 Fehler & Feature-Wünsche

Bitte gib folgende Informationen an:

- Home-Assistant-Version
- BTC-Calc-Card-Version
- Aktuelle Konfiguration
- Relevante Fehlermeldungen
- Kurze Beschreibung des Problems

Bitte entferne persönliche oder sensible Daten aus Konfigurationen und Logs.

Erstelle ein [GitHub Issue](https://github.com/jinx-22/btc-calc-card/issues).

---

# 🧡 Unterstützung & Spenden

<div align="center">

### <a id="lightning"></a>Lightning

<img width="32" alt="Lightning" src="https://github.com/user-attachments/assets/0bff59d2-7986-46cf-9d39-17fe0dbb128a" />

`usefulplay52@walletofsatoshi.com`

<img height="300" alt="Lightning - Wallet of Satoshi" src="https://github.com/user-attachments/assets/65cc18d9-05d1-4a00-8ccc-9922fdb54baf" />

### <a id="bitcoin"></a>Bitcoin

<img width="32" alt="Bitcoin" src="https://github.com/user-attachments/assets/f74cad36-8c05-4a33-89cd-b998075af33b" />

`bc1qkz7mtp23cmshxnru96lzgeayu0urlysvqk5vry`

<img height="300" alt="Bitcoin donation" src="https://github.com/user-attachments/assets/196f68e4-b0e8-4f27-bded-8c4fe13b9d45" />

</div>

Danke für deine Unterstützung — ein kostenloser ⭐ hilft anderen, das Projekt zu entdecken:

[![stars](https://img.shields.io/github/stars/jinx-22/btc-calc-card)](https://github.com/jinx-22/btc-calc-card/stargazers)

---
# 📜 Lizenz

**Apache-2.0**

---

Mit ❤️ für Home Assistant gemacht
