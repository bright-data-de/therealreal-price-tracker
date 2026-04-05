# The RealReal Preis-Tracker

[![Bright Data](https://img.shields.io/badge/Powered%20by-Bright%20Data-blue?style=flat-square)](https://brightdata.de)
[![The RealReal Price Tracker](https://img.shields.io/badge/The%20RealReal%20Price%20Tracker-Managed%20Solution-orange?style=flat-square)](https://brightdata.de/products/insights/price-tracker/therealreal)
[![Python](https://img.shields.io/badge/Python-3.9%2B-yellow?style=flat-square)](https://python.org)

[![Bright Insights Price Tracker](https://raw.githubusercontent.com/danielshashko/bright-insights-assets/main/price-tracker-hero-v2.png)](https://brightdata.de/products/insights/price-tracker/therealreal)

Echtzeit-Preisverfolgung für The RealReal – ein Online-Marktplatz für Luxus-Kommissionsware. Zwei Möglichkeiten für den Einstieg: eine **vollständig verwaltete** Intelligence-Plattform oder eine **Self-Service-API**, um Ihre eigene Pipeline zu erstellen.

---

## Option 1: Bright Insights - KI-gestütztes Price Tracking (Empfohlen)

**[Bright Insights](https://brightdata.de/products/insights/price-tracker/therealreal)** ist die vollständig verwaltete Retail-Intelligence-Plattform von Bright Data. Keine Scraper, die erstellt werden müssen, keine Infrastruktur, die gewartet werden muss – nur strukturierte, analysebereite Preisdaten, die an Dashboards, Data Feeds oder Ihre BI-Tools geliefert werden.

**Warum Teams Bright Insights wählen:**
- 🚀 **Kein Setup** – In wenigen Minuten live mit sofort einsatzbereiten Dashboards und Data Feeds
- 🤖 **KI-gestützte Empfehlungen** – Ein konversationeller KI-Assistent verwandelt Millionen von Datenpunkten sofort in umsetzbare Erkenntnisse
- ⚡ **Echtzeit-Monitoring** – Aktualisierungsraten von stündlich bis täglich mit sofortigen Benachrichtigungen (E-Mail, Slack, webhook)
- 🌍 **Unbegrenzte Skalierung** – Jede Website, jede Geografie, jede Aktualisierungsfrequenz
- 🔗 **Plug-and-play-Integrationen** – AWS, GCP, Databricks, Snowflake und mehr
- 🛡️ **Vollständig verwaltet** – Bright Data übernimmt Schemaänderungen, Website-Updates und Datenqualität automatisch

**Wichtige Anwendungsfälle:**
- ✅ **Wiederverkaufswert-Trends verfolgen** auf The RealReal
- ✅ **Angebots- und Verkaufspreise überwachen** für bestimmte Artikel
- ✅ **Arbitrage-Möglichkeiten identifizieren** zwischen Plattformen
- ✅ Einhaltung der MAP-Richtlinie überwachen und Preisverstöße erkennen
- ✅ Wettbewerber-Promotions und Promotionsdynamiken verfolgen
- ✅ Saubere, harmonisierte Daten direkt in dynamische Preisalgorithmen oder KI-Modelle einspeisen

> **Ab $250/Monat – [Individuelles Angebot anfordern →](https://brightdata.de/products/insights/price-tracker/therealreal)**

---

## Option 2: Self-Service über Web Scraper API

Möchten Sie lieber Ihre eigene Pipeline erstellen? Die **Web Scraper API** von Bright Data bietet Ihnen programmatischen Zugriff auf The RealReal-Produktdaten – Preise, Verfügbarkeit, Bewertungen und mehr – ohne dass Sie Proxys oder Scraping-Infrastruktur verwalten müssen.

### Voraussetzungen

- Python 3.9 oder höher
- Ein [Bright Data account](https://brightdata.de) (kostenlose Testversion verfügbar)
- Ein Bright Data **API token** ([so erhalten Sie einen](https://docs.brightdata.de/general/account/account-settings#api-token))
- Eine Bright Data **Web Scraper ID** für The RealReal-Produkte ([finden Sie Ihre im Web Scrapers Control Panel](https://brightdata.de/cp/scrapers))

### Einrichtung

1. **Dieses repository klonen**

   ```bash
   git clone https://github.com/bright-data-de/therealreal-price-tracker.git
   cd therealreal-price-tracker
   ```

2. **Abhängigkeiten installieren**

   ```bash
   pip install -r requirements.txt
   ```

3. **Zugangsdaten konfigurieren**

   Kopieren Sie `.env.example` nach `.env` und tragen Sie Ihre Werte ein:

   ```bash
   cp .env.example .env
   ```

   ```env
   BRIGHTDATA_API_TOKEN=your_api_token_here
   BRIGHTDATA_DATASET_ID=your_dataset_id_here
   ```

   > **Ihre Web Scraper ID finden**
   > Melden Sie sich im [Bright Data Control Panel](https://brightdata.de/cp/scrapers) an, navigieren Sie zu **Web Scrapers**,
   > suchen Sie nach "The RealReal" und kopieren Sie die Web Scraper ID (Format: `gd_xxxxxxxxxxxx`).

---

## Verwendung

### 1. Bestimmte Produkte per URL verfolgen

Übergeben Sie eine Liste von The RealReal-Produkt-URLs, um strukturierte Preisdaten abzurufen:

```python
from price_tracker import track_prices

urls = [
    "https://www.therealreal.com/product/sample-item-123456",
    # Add more product URLs here
]

results = track_prices(urls)
for item in results:
    print(f"{item.get('title')} - {item.get('final_price', item.get('price'))} {item.get('currency', '')}")
```

Oder direkt ausführen:

```bash
python price_tracker.py
```

### 2. Produkte per Keyword entdecken

Finden Sie Produkte, die einer Keyword-Suche entsprechen:

```python
from price_tracker import discover_by_keyword

results = discover_by_keyword("laptop", limit=50)
```

### 3. Produkte per Kategorie-URL durchsuchen

Sammeln Sie alle Produkte von einer The RealReal-Kategorieseite:

```python
from price_tracker import discover_by_category

results = discover_by_category(
    "https://therealreal.com/category/example",
    limit=100,
)
```

---

## Ausgabefelder

Jeder Ergebnisdatensatz enthält die folgenden Felder:

| Field | Description |
|-------|-------------|
| `url` | Listing-URL |
| `title` | Artikeltitel |
| `brand` | Marke |
| `price` | Gelisteter Preis |
| `currency` | Währungscode |
| `condition` | Artikelzustand (neu/gebraucht/etc.) |
| `size` | Größe (falls zutreffend) |
| `seller_name` | Verkäufer-Benutzername |
| `seller_rating` | Verkäuferbewertung |
| `images` | Artikelbild-URLs |
| `description` | Artikelbeschreibung |
| `timestamp` | Zeitstempel der Erfassung |

### Beispielausgabe

```json
[
  {
    "url": "https://www.therealreal.com/product/sample-item-123456",
    "title": "Example Product Name",
    "brand": "Example Brand",
    "initial_price": 59.99,
    "final_price": 44.99,
    "currency": "USD",
    "discount": "25%",
    "in_stock": true,
    "rating": 4.5,
    "reviews_count": 1234,
    "images": ["https://therealreal.com/images/product1.jpg"],
    "description": "Product description text...",
    "timestamp": "2025-01-15T10:30:00Z"
  }
]
```

---

## Erweiterte Optionen

Die Funktion `trigger_collection()` akzeptiert optionale Parameter zur Steuerung der Datenerfassung:

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `limit` | integer | - | Maximale Anzahl der zurückzugebenden Datensätze |
| `include_errors` | boolean | `true` | Fehlerberichte in die Ergebnisse einschließen |
| `notify` | string (URL) | - | Webhook-URL, die aufgerufen wird, wenn der Snapshot bereit ist |
| `format` | string | `json` | Ausgabeformat: `json`, `csv` oder `ndjson` |

Beispiel mit Optionen:

```python
from price_tracker import trigger_collection, get_results

inputs = [{"url": "https://www.therealreal.com/product/sample-item-123456"}]
snapshot_id = trigger_collection(inputs, limit=200, notify="https://your-webhook.com/hook")
results = get_results(snapshot_id)
```

---

## Ressourcen

- 🌟 [The RealReal Price Tracker - Bright Insights (Managed)](https://brightdata.de/products/insights/price-tracker/therealreal)
- 🔧 [The RealReal Scraper API](https://brightdata.de/products/web-scraper/therealreal)
- 📖 [Bright Data Web Scraper API Documentation](https://docs.brightdata.de/scraping-automation/web-scraper-api/overview)
- 🗄️ [Web Scrapers Control Panel](https://brightdata.de/cp/scrapers)
- 🔑 [How to get an API token](https://docs.brightdata.de/general/account/account-settings#api-token)
- 🌐 [Bright Data Homepage](https://brightdata.de)

---

*Erstellt mit [Bright Data](https://brightdata.de) – der branchenführenden Webdaten-Plattform.*