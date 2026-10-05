## 2. `LICENSES.md`

```markdown
# Third-Party Open-Source & API Compliance Register

This register details all dependent open-source libraries, frameworks, APIs, and hardware firmware licenses used across the system to ensure complete legal compliance for open sharing or commercial repurposing[cite: 1, 4].

| Component / Dependency | Domain / Module | License Type | Commercial Reuse Terms & Rate Limits |
| :--- | :--- | :--- | :--- |
| **Supabase** | Managed Database & Auth | Apache License 2.0 / PostgreSQL License | Fully permissive for commercial SaaS, modification, and distribution[cite: 1, 4]. |
| **WLED Firmware** | LED Controller Firmware | MIT License | Permissive; permits commercial usage provided copyright notices are retained[cite: 1, 4]. |
| **Tailwind CSS** | Web UI Styling | MIT License | Permissive; open commercial distribution permitted. |
| **Discogs API** | Catalogue Data Engine | Discogs API Terms of Use | Non-commercial rate limit: 60 requests/minute (authenticated)[cite: 1, 4]. Commercial redistribution requires formal licensing agreement[cite: 1, 4]. |
| **Last.fm API** | Track Scrobbling & Playback | Last.fm API Terms of Service | Free for non-commercial personal scrobbling[cite: 1, 3]. Requires explicit attribution[cite: 1]. Commercial licensing required for standalone apps. |
| **Tasker Platform** | Android Automation Engine | Proprietary License (Paid Application) | Requires user license on target Android devices[cite: 1, 3, 7]. |
| **Apple Shortcuts** | iOS Automation Engine | Proprietary Apple System Feature | Integrated natively into iOS; no licensing constraints for URL handling[cite: 1, 3, 7]. |

---

## Open-Source Attribution Guidelines
Upon public GitHub distribution or commercial pivot:
1. Include unmodified copies of all MIT and Apache 2.0 license headers in code sources[cite: 1].
2. Ensure no hardcoded local IP addresses, private Supabase service-role keys, or API secrets exist in public commits[cite: 1, 4].
3. Maintain clear attribution to Discogs and Last.fm for external metadata feeds[cite: 1].