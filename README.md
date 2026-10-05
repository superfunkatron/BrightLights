# BrightLights
A home vinyl organisation and search project.
🎵📚

An interactive smart library system designed for an extensive vinyl record collection housed in IKEA Kallax units. The system combines physical spatial mapping, addressable LED lighting, NFC deep-linking, and a custom web search interface.

## System Features
* **Web UI (Google Stitch Design):** Mobile-first, vinyl-shop aesthetic for guests to search albums and track titles without logging in.
* **Relational Database (Supabase):** Houses collection metadata, tracklists, and physical Kallax cube coordinates.
* **Smart Shelf LEDs (WLED / ESP32):** Triggers addressable 12V LED strips to illuminate the exact physical shelf location when an album is selected or scanned.
* **NFC Quick-Scanning:** Mounted NTAG215 cards deep-link directly to shelf views in the web app.

## Tech Stack
* **Frontend:** Static Web App (HTML/CSS/JS) hosted on GitHub Pages.
* **Database & API:** Supabase (PostgreSQL & PostgREST Data API).
* **Hardware Controller:** MagWLED (ESP32 running WLED firmware).
* **Catalog Data Source:** Discogs API & Oggee Club exports.

## Repository Structure
* `/supabase` - SQL schema migrations (`cubes`, `records`, `tracks`).
* `/src` - Client-side web application source code.
* `ARCHITECTURE.md` - System layout, relational schemas, and WLED API contracts.
* `LICENSES.md` - Third-party API terms and open-source license register.
