# Hardware Assembly & Maintenance Standard Operating Procedure

## 1. System Hardware Specifications
* **Primary Controller:** MagWLED-2 Board (ESP32-S3 microcontroller running WLED) mounted behind DJ mixer in Unit C[cite: 1, 3].
* **Power Supply Unit (PSU):** 12V DC power supply wired to screw terminals[cite: 1, 2, 5].
* **Addressable Lighting:** 12V Addressable LED Strips (WS2815 / 12V COB)[cite: 1, 2, 3].
* **Mounting Profiles:** Matte black aluminum channels with opal/frosted diffusers[cite: 1, 2, 3].
* **Wiring Harness:** 3-conductor 20AWG black micro-cables routed along rear interior seams[cite: 1, 2, 3].

---

## 2. Power Channel Routing & Physical Cabling

### Output 1 Wiring (Dedicated Unit A)
* Runs directly from MagWLED-2 Output 1 screw terminal to **Unit A** (White 4x4 Kallax, 16 Cubes)[cite: 1, 2].
* Covers 16 LED segments wired in series along the front underside of each cube grid[cite: 1, 2, 3].

### Output 2 Wiring (Units C & B Daisy-Chain)
* Runs from MagWLED-2 Output 2 screw terminal to **Unit C** (Horizontal 2x4 DJ Console, 8 Cubes)[cite: 1, 2].
* Extends from the end of Unit C across a ~30cm physical gap via a concealed 3-conductor bridge cable to **Unit B** (Vertical 1x4 Kallax, 4 Cubes)[cite: 1].
* 
[MagWLED-2 Controller]
├── (Output 1) ───> [Unit A: 4x4 Kallax (16 Cubes)]
└── (Output 2) ───> [Unit C: 2x4 Kallax (8 Cubes)] ───(30cm Gap Bridge)───> [Unit B: 1x4 Kallax (4 Cubes)]

---

## 3. Physical Assembly Guidelines

1. **Profile Installation:** Cut matte black aluminum profiles to exact interior cube widths. Secure profiles under the front top lip of each Kallax cube, pointing LEDs backward at an angle toward the record spines to provide indirect, diffused lighting[cite: 2, 3].
2. **Vinyl Backstops:** Cut high-density EVA foam backstop blocks and insert them at the rear of each cube[cite: 1, 4]. This ensures all record spines sit flush at the front edge of the shelf for uniform illumination[cite: 1, 2].
3. **Wire Concealment:** Route 3-conductor cabling along the rear interior corner joints of each cube frame, secured with micro wire-clips completely hidden behind the record sleeves[cite: 2, 3].

---

## 4. Maintenance & Troubleshooting Procedures

### Procedure A: WLED Controller Disconnection
1. Verify status LED on the MagWLED-2 board[cite: 2, 5].
2. If offline, power cycle the 12V power supply.
3. Access local Wi-Fi router management page to confirm IP reservation for `<magwled_ip>`[cite: 2, 5].
4. Open browser to `http://<magwled_ip>` to verify WLED web UI interface[cite: 2, 5].

### Procedure B: Individual Cube Segment Failure
1. Inspect 3-wire micro-connector leading to the non-responsive cube profile[cite: 2, 5].
2. Check WLED Segment Config: ensure segment bounds (`start_index` to `stop_index`) match database parameters in `ARCHITECTURE.md`[cite: 1, 2].
3. If downstream segments beyond a specific point fail, replace the first non-responsive LED profile section (WS2815 dual-data lines protect downstream LEDs against single-chip failures)[cite: 2].