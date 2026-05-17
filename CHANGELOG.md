# Changelog – heimeliQ Furniture Template

Versionierung folgt [Semantic Versioning](https://semver.org/lang/de/).

- **MAJOR** (`x.0.0`): Breaking Change. Bestehende Möbel-Repos brauchen Migration.
- **MINOR** (`0.x.0`): Neues optionales Feld oder Ordner. Bestehende Repos funktionieren weiter.
- **PATCH** (`0.0.x`): Tippfehler, Klarstellungen, Bug-Fixes, kein strukturelles Update.

## [0.2.0] – Wald-Namensgeber, schlankeres ID-Schema

Jedes heimeliQ-Möbel trägt den Namen eines real existierenden Waldes. Der Waldname ist möbel-eindeutig: kein zweites Möbel trägt denselben Wald. Damit wird die Marke um eine inhaltliche Schicht erweitert – jedes Möbel verweist auf einen Ort und macht bei bedrohten Wäldern deren Situation sichtbar. Da der Waldname allein eindeutig ist, entfällt das `<typ>`-Segment in der ID.

**Neu:**

- ID-Schema umgestellt von `heimeliq-<reihe>-<typ>-<nr>` auf `heimeliq-<reihe>-<waldname>`.
- `heimeliq.toml` bekommt eine `[forest]`-Section mit Pflichtfeldern (`id`, `name`, `region`, `country`) und optionalen Feldern (`forest_type`, `age_estimate_years`, `status`, `themes`, `links`, `note`).
- `type` bleibt erhalten, jetzt aber als Metadatenfeld für Filter/Suche – nicht mehr als Teil der ID.
- Neues optionales `tags`-Array für zusätzliche Schlagworte.
- `heimeliq.schema.json` validiert `forest` als Pflicht-Section und prüft den `slug`-Pattern auf `<reihe>-<waldname>`.
- README erklärt das Wald-Konzept und die Typ/Tags-Logik.
- `README.example.md` enthält einen prominenten Wald-Namensgeber-Bereich.

**Migration für bestehende Möbel-Repos (z. B. das v0.1.x-Pilotmöbel):**

1. Repo umbenennen auf `heimeliq-<reihe>-<waldname>`.
2. In `heimeliq.toml`: `slug` anpassen, `[forest]`-Section ergänzen, ggf. `tags` setzen.
3. `heimeliq-template-version` auf `0.2.0` setzen.
4. Validate-Action laufen lassen.

## [0.1.1] – TOML-Reihenfolge-Bugfix in `okh.toml`

Behebt einen latenten Bug in der Beispiel-`okh.toml`: Einige Top-Level-Felder (`mass`, `manufacturing-instructions`, `bom`, `readme`) standen nach Section-Headern und wurden dadurch laut TOML-Spezifikation als Sub-Felder dieser Sections interpretiert. Dasselbe galt für `[part.outer-dimensions]`, das bei mehreren `[[part]]`-Einträgen mehrdeutig wird.

**Behoben:**

- Alle Top-Level-Felder stehen jetzt vor der ersten Section.
- `outer-dimensions` innerhalb `[[part]]` wird als Inline-Table notiert.
- Erklärender Kommentar zur TOML-Reihenfolge in der Datei ergänzt.

## [0.1.0] – initial

- Erste Version des Templates.
- OKH 2.4 als Standard für Möbel-Metadaten.
- **Lizenz-Trennung**: Template selbst unter MIT, daraus erzeugte Möbel-Repos unter CERN-OHL-S-2.0.
- `LICENSE.example` und `README.example.md` als Vorlagen.
- Doku-Struktur unter `docs/de/` mit co-located `.images/`-Ordnern.
- `heimeliq.toml` für projektspezifische Erweiterungen.
- `heimeliq.schema.json` für strenge Validierung.
- GitHub-Action `validate.yml` mit kontextabhängigen Checks.
- REUSE-konforme Datei-Lizenzangaben.
