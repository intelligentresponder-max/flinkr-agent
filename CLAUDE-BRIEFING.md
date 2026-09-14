# Übergabe: flinkr-agent

**Repo:** https://github.com/intelligentresponder-max/flinkr-agent.git
**Ziel-URL:** https://intelligentresponder-max.github.io/flinkr-agent/
**Aufgabe:** Landingpage für Flink-Gutscheincode `FLINK-MPDEUA` live bringen und pflegen.

## Sofort prüfen (bekanntes Problem)
Die Seite liefert aktuell **404** auf der GitHub-Pages-URL. Wahrscheinliche Ursache:
Datei wurde in der GitHub-Mobilansicht umbenannt, Groß-/Kleinschreibung oder Endung
stimmt vermutlich nicht exakt (`index.html`, alles klein, kein Leerzeichen).

```bash
git clone https://github.com/intelligentresponder-max/flinkr-agent.git
cd flinkr-agent
ls -la
```

- Existiert `index.html` (exakt so, klein) im Root? Falls nicht → korrekt umbenennen:
  ```bash
  git mv <falscher-name> index.html
  git commit -m "fix: index.html korrekt benannt"
  git push
  ```
- GitHub Pages Einstellung prüfen: Settings → Pages → Source = `main` / `(root)`.
- Nach Push 1–2 Min. warten, dann `curl -I https://intelligentresponder-max.github.io/flinkr-agent/` → muss `200` liefern.

## Über die Datei
Single-File HTML, kein Build-Prozess, keine Frameworks (React/Vue bewusst vermieden).
- Tailwind via CDN, Fonts: Fraunces (Display) + Public Sans (Body) + IBM Plex Mono (Code/Zähler)
- Sprachen: DE, EN, FR, ES, IT, PL über `i18n`-Objekt im `<script>`-Block, Umschalter oben
- Zähler "noch X von 50": rein clientseitig über `localStorage`, zählt bei Klick auf
  "Code kopieren" runter. **Keine echten Flink-Einlösungsdaten** — im Text klar als
  lokale Schätzung gekennzeichnet, das bitte beim Weiterbauen so belassen.
- SEO/GEO: JSON-LD `Offer` + `FAQPage` im `<head>`, Meta-Description/Keywords auf
  Frankfurt + Flink-Lieferstädte ausgerichtet

## Negative Constraints (Vertical-Coding-Leitfaden)
- Kein React/Vue/schweres Framework
- Keine Inline-Styles außerhalb Tailwind-Klassen
- Keine Platzhalter-/Lorem-Ipsum-Inhalte
- Änderungen möglichst per `sed`/`git mv` direkt im Repo statt Download/Upload-Zyklus

## Fehlerprotokoll (bitte weiterführen)
- 14.09.2026: Datei beim manuellen Upload über GitHub-Mobilweb als `index` ohne
  Endung angelegt → GitHub Pages konnte nicht ausliefern (404). Lehre: bei
  Mobil-Uploads Dateiname im Commit-Dialog immer vor dem Absenden explizit
  gegenprüfen, nicht nur den Upload-Dialog.

## Nächster Schritt für Claude Code
1. Root-Verzeichnis inspizieren, tatsächlichen Dateinamen feststellen
2. Falls nötig korrigieren und pushen
3. Live-Check per `curl -I`
4. Danach: Repo-Struktur aufräumen (README.md ergänzen, `.gitignore` falls nötig)
