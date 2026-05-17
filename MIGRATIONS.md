# Migrationsanleitungen

Wenn diese Vorlage auf eine neue **Major-Version** gehoben wird (z. B. `0.x.x` → `1.0.0`), beschreibt dieser Abschnitt, was bestehende Möbel-Repos tun müssen, um auf die neue Vorlagen-Version umzustellen.

Bestehende Repos werden nicht automatisch migriert – Stabilität geht vor.

## Reihenfolge bei einer Migration

1. Im Möbel-Repo einen Branch `migration-template-x.y.z` anlegen.
2. Diesem Dokument folgen.
3. Lokale Validierung laufen lassen (siehe `validate.yml`).
4. Im Möbel-Repo `heimeliq.toml` → `heimeliq-template-version` auf neue Version setzen.
5. Eintrag in `changelog.md` (klein, im Möbel-Repo) ergänzen.
6. Branch mergen, neuen SemVer-Tag setzen.

---

## 0.1.x → 0.2.0

Diese Version führt das **Wald-Namensgeber-Konzept** ein und verschlankt das ID-Schema. Bestehende Möbel-Repos (typischerweise das v0.1.x-Pilotmöbel) sollten so migriert werden:

1. **Repo umbenennen** auf das neue Schema `heimeliq-<reihe>-<waldname>`. Beispiel: `heimeliq-massiq-sideboard-001` → `heimeliq-massiq-hambach`. Auf GitHub geht das in den Settings; die alte URL bleibt eine Weile als Redirect bestehen.

2. **`heimeliq.toml` anpassen**:
   - `slug` auf `<reihe>-<waldname>` setzen (z. B. `"massiq-hambach"`).
   - `type` bleibt erhalten, aber jetzt als Metadatenfeld (z. B. `"sideboard"`).
   - Optional: `tags = ["..."]` ergänzen.
   - Neue Pflicht-Section `[forest]` ergänzen – mindestens `id`, `name`, `region`, `country` ausfüllen. Optionale Felder (`forest_type`, `age_estimate_years`, `status`, `themes`, `links`, `note`) nach Möglichkeit ebenfalls befüllen.
   - `heimeliq-template-version` auf `"0.2.0"` heben.

3. **README im Möbel-Repo aktualisieren**: Den Wald-Namensgeber-Bereich aus der neuen `README.example.md` übernehmen und ausfüllen.

4. **Validate-Action lokal oder via Push prüfen**: Schlägt die Validierung an, fehlt vermutlich ein Pflichtfeld in `[forest]` oder der `slug` passt nicht zum neuen Pattern.

5. **`furniture-repos.json` im Website-Repo aktualisieren**: Die alte URL gegen die neue tauschen.

6. **CHANGELOG.md des Möbels** (klein, im Möbel-Repo) ergänzen mit einem Eintrag wie:

   ```
   ## [0.2.0] – Wald-Namensgeber ergänzt, Repo umbenannt
   - Repo-Name: heimeliq-massiq-sideboard-001 → heimeliq-massiq-hambach
   - [forest]-Section in heimeliq.toml ergänzt
   - Template-Version 0.2.0
   ```

---

## 0.x → 1.0 (noch nicht erschienen)

*Wird ergänzt, sobald die erste Major-Version veröffentlicht wird.*
