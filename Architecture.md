# Vinyl Library Smart System: System Architecture & Data Schema

## 1. System Overview & Physical Layout
The system transforms a 32-cube IKEA Kallax setup into an interactive, smart vinyl library using addressable 12V LED lighting, NFC tags, and a custom web application[cite: 2, 3].

### Physical Furniture Priority & Spatial Mapping
* **Unit A:** 4x4 Kallax (16 Cubes: `001A`–`004D` / `A1_1`–`A4_4`) at the main station[cite: 1, 3].
* **Unit C:** 2x4 Kallax horizontal DJ console (8 Cubes: `005A`–`006D` / `C1_1`–`C2_4`)[cite: 1, 3].
* **Unit B:** 1x4 Kallax vertical shelf (4 Cubes: `007A`–`010A` / `B1_1`–`B1_4`)[cite: 1, 3].
* **Unit D:** 2x4 Kallax (8 Cubes: `011A`–`011D` / `D1_1`–`D2_4`, deferred across the apartment)[cite: 1, 3].

---

## 2. Relational Database Schema (Supabase PostgreSQL)

### Table: `cubes`
Stores physical location properties, friendly folder names, and hardware mapping parameters[cite: 1].

| Column Name | Data Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `cube_id` | `TEXT` | `PRIMARY KEY` | Standard folder code (e.g., `"001A"`, `"001B"`)[cite: 1]. |
| `unit` | `TEXT` | `NOT NULL` | Physical unit identifier (`"Unit A"`, `"Unit C"`, `"Unit B"`)[cite: 1]. |
| `row_index` | `INT` | `NOT NULL` | Physical grid row index (1 to 4)[cite: 1]. |
| `col_index` | `INT` | `NOT NULL` | Physical grid column index (1 to 4)[cite: 1]. |
| `friendly_label` | `TEXT` | `NOT NULL` | User-facing genre/folder label (e.g., `"Bangers"`, `"Indie"`)[cite: 1, 6]. |
| `discogs_folder_id` | `INT` | `UNIQUE` | Corresponding 1:1 Discogs folder ID[cite: 1, 3]. |
| `wled_output_channel` | `INT` | `NOT NULL` | Controller pin channel (`1` or `2`)[cite: 1, 2]. |
| `wled_segment_id` | `INT` | `NOT NULL` | Addressable LED array segment index[cite: 1, 2]. |
| `led_start_index` | `INT` | `NOT NULL` | Starting LED pixel index in strip segment[cite: 2]. |
| `led_stop_index` | `INT` | `NOT NULL` | Ending LED pixel index in strip segment[cite: 2]. |

### Table: `records`
Stores album metadata and physical cube locations[cite: 1].

| Column Name | Data Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `discogs_id` | `BIGINT` | `PRIMARY KEY` | Unique Discogs master/release catalog ID[cite: 1]. |
| `title` | `TEXT` | `NOT NULL` | Album title[cite: 1, 6]. |
| `artist` | `TEXT` | `NOT NULL` | Artist or ensemble name[cite: 1, 6]. |
| `catalog_number` | `TEXT` | `NULLABLE` | Release catalog number[cite: 6]. |
| `format_description`| `TEXT` | `NULLABLE` | Format descriptor (e.g., `12", LP, Album, RE`)[cite: 6]. |
| `cube_id` | `TEXT` | `REFERENCES cubes(cube_id)` | Foreign key linking record to current physical cube location[cite: 1]. |
| `status` | `TEXT` | `DEFAULT 'HOUSED'` | Options: `HOUSED`, `IN_TRANSIT` (Folder 000), `UNHOUSED` (Folder 0000)[cite: 1, 6]. |

### Table: `tracks`
Stores parsed tracklist metadata for song search indexing[cite: 1, 6].

| Column Name | Data Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `track_id` | `UUID` | `PRIMARY KEY, DEFAULT gen_random_uuid()` | System track ID. |
| `discogs_id` | `BIGINT` | `REFERENCES records(discogs_id)` | Link to album record. |
| `position` | `TEXT` | `NOT NULL` | Track side/number (e.g., `"A1"`, `"B2"`). |
| `title` | `TEXT` | `NOT NULL` | Song title[cite: 6]. |
| `bpm` | `INT` | `NULLABLE` | Track tempo[cite: 3, 6]. |
| `musical_key` | `TEXT` | `NULLABLE` | Musical key[cite: 3, 6]. |

---

## 3. Local API & Controller Contracts

### WLED HTTP JSON Trigger Specification
* **Transport Protocol:** Wi-Fi over local 2.4GHz network (`HTTP POST`)[cite: 2, 5].
* **Controller Endpoint:** `http://<magwled_ip>/json/state`[cite: 2, 5]
* **Target Payload (Illuminate Cube `001A`):**

```json
{
  "on": true,
  "bri": 255,
  "transition": 5,
  "seg": [
    {
      "id": 0,
      "start": 0,
      "stop": 19,
      "col": [[255, 180, 50]],
      "fx": 0
    }
  ]
}