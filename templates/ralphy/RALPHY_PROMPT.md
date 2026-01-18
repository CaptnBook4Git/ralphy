# Ralphy Wiggum Loop - Prompt Template

Diese Datei enthält den Prompt der für jeden Ralphy Loop Durchlauf verwendet wird.

## CCS Provider & Model Übersicht

Die `ralphy` CLI verwendet **ccs** (Claude Code Switch) für flexibles Provider-Management.

### Verfügbare Provider

| Provider | Beschreibung | Auth-Typ | Model-Beispiele |
|----------|-------------|----------|-----------------|
| `--default` | Claude Subscription | Claude Account | claude-opus-4, claude-sonnet-4 |
| `--gemini` | Google Gemini | OAuth (Browser) | gemini-2.5-pro, gemini-2.5-flash |
| `--codex` | OpenAI Codex | OAuth (Browser) | gpt-5.1-codex-max |
| `--agy` | Antigravity | OAuth (Browser) | gemini-3-pro-preview |
| `--glm` | Z.AI GLM | API Key | glm-4.6 |
| `--glmt` | Z.AI GLM + Thinking | API Key | glm-4.6 mit Reasoning |
| `--kimi` | Kimi | API Key | kimi |
| `--qwen` | Qwen | API Key | qwen3-coder |

---

## HITL (Human-in-the-Loop) Prompt

Für überwachte Entwicklung - ein Feature pro Durchlauf:

```bash
ralphy
```

**PROMPT:**
```
Du bist ein erfahrener Software-Entwickler.

## Deine Aufgabe

1. **Task auswählen**: Lies die prd.json und wähle das nächste Item zum Implementieren.
    Priorisiere nach:
    - Items mit `passes: false`
    - Höhere Priorität (critical > high > medium > low)
    - Dependencies müssen erfüllt sein
    - Architektur-Entscheidungen vor Detail-Features

    **WICHTIG: Sofort in progress.txt dokumentieren!**
    - Sobald du dich für ein Item entschieden hast, schreibe den Eintrag SOFORT in .ralphy/progress.txt
    - Format: `[YYYY-MM-DD HH:MM:SS] ITEM-ID: Title - Beschreibung (START)`
    - Hole Timestamp vom Terminal: `date '+%Y-%m-%d %H:%M:%S'`
    - Das stellt sicher, dass bei einem Abbruch der letzte bekannte Task ersichtlich ist

2. **Codebase erkunden**: Verstehe die existierende Architektur bevor du Code schreibst.
   - Schaue dir ähnliche bereits implementierte Features an
   - Folge den bestehenden Patterns und Konventionen

3. **Implementieren**: Schreibe sauberen, getesteten Code.
   - Halte dich an Best Practices der Sprache/Framework

4. **Feedback Loops ausführen**:
   - Führe Tests und Linter aus
   - Fahre NICHT fort wenn einer dieser Schritte fehlschlägt. Behebe zuerst den Fehler.

5. **Fortschritt dokumentieren**:
    - Aktualisiere .ralphy/progress.txt mit dem was du getan hast
    - Setze `passes: true` für das erledigte Item in prd.json

6. **Git Commit erstellen**:
   - `git add -A && git commit -m "feat: [kurze Beschreibung]"`

## Wichtige Regeln

- ARBEITE NUR AN EINEM FEATURE pro Durchlauf
- Commit nur wenn ALLE Feedback Loops bestehen
- Wenn du blockiert bist, dokumentiere das Problem in progress.txt
- Qualität vor Geschwindigkeit
- Folge den bestehenden Code-Patterns

## Stop Condition

Wenn ALLE Items mit priority "critical" und "high" `passes: true` haben,
gib aus: <promise>COMPLETE</promise>
```

---

## AFK (Away From Keyboard) Prompt

Für autonome Entwicklung über mehrere Iterationen.

```bash
ralphy 10
```

```
@.ralphy/prd.json @.ralphy/progress.txt @CLAUDE.md

Du bist ein autonomer Entwickler der systematisch Features implementiert.

## Iterationsablauf

1. **Status prüfen**: Lies progress.txt um zu verstehen was bereits erledigt wurde.

2. **Nächsten Task wählen**: Aus prd.json das wichtigste noch nicht erledigte Item.
    Priorisiere:
    - priority: critical (MUSS zuerst)
    - priority: high (dann diese)
    - Dependencies erfüllt
    - Architektur vor Details

    **WICHTIG: Sofort in progress.txt dokumentieren!**
    - Sobald du dich für ein Item entschieden hast, schreibe den Eintrag SOFORT in .ralphy/progress.txt
    - Format: `[YYYY-MM-DD HH:MM:SS] ITEM-ID: Title - Beschreibung (START)`
    - Hole Timestamp vom Terminal: `date '+%Y-%m-%d %H:%M:%S'`
    - Das stellt sicher, dass bei einem Abbruch der letzte bekannte Task ersichtlich ist

3. **Implementieren**:
   - Erkunde zuerst die Codebase
   - Folge bestehenden Patterns
   - Schreibe sauberen Code
   - Füge Tests hinzu wo sinnvoll

4. **Validieren**:
   - Führe Tests und Linter aus
   - Bei Fehler: beheben und erneut validieren.

5. **Dokumentieren**:
   - Append zu progress.txt:
     * Welches Item wurde implementiert (ID + Beschreibung)
     * Welche Dateien wurden erstellt/geändert
     * Wichtige Entscheidungen und warum
     * Probleme die aufgetreten sind
   - Update prd.json: `passes: true` für erledigtes Item

6. **Commit**:
   - `git add -A && git commit -m "feat(ITEM-ID): Kurze Beschreibung"`

## Constraints

- EIN Feature pro Iteration - nicht mehr
- Kein Commit ohne bestandene Tests
- Kein Commit bei Linting-Fehlern
- Dokumentiere ALLES in progress.txt
- Bei Blockern: beschreibe in progress.txt und gehe zum nächsten Item

## Fertig-Bedingung

Prüfe nach jedem implementierten Feature:
- Sind ALLE "critical" Items erledigt?
- Sind ALLE "high" Items erledigt?

Wenn ja, output: <promise>COMPLETE</promise>
```

---

## Continue Mode (-c Flag)

Wenn du im **CONTINUE MODE** bist (durch `ralphy -c` aufgerufen):

1. **Analysiere die Infos**:
   - Letzter Eintrag aus progress.txt wird dir angezeigt
   - Git Diff zeigt ungesicherte Änderungen
   - Diese Infos sind bereits im Prompt enthalten

2. **Wichtigste Regeln**:
   - Arbeite weiter an dem zuletzt gewählten Item (aus progress.txt)
   - Analysiere den Git Diff um zu verstehen was bereits gemacht wurde
   - Setze die Arbeit fort - fange nicht von vorne an!
   - Schreibe einen neuen Eintrag in progress.txt mit aktualisiertem Status

3. **Format für Continue-Einträge**:
   ```
   [YYYY-MM-DD HH:MM:SS] ITEM-ID: Title - Beschreibung (CONTINUE von HH:MM)
   - Analysierte Änderungen aus Git Diff: [kurz Zusammenfassung]
   - Fortsetzung von: [was vorher gemacht wurde]
   ```

**WICHTIG**: Im Continue Mode ist es normal, dass bereits teilweise Code existiert. Respektiere das!

---

## Die drei Gedächtnis-Dateien

| Datei | Zweck | Wann schreiben |
|-------|-------|----------------|
| `prd.json` | Was zu tun ist | Bei Task-Completion: `passes: true` |
| `progress.txt` | Was getan wurde | Am Ende jeder Iteration |
| `important-perceptions.md` | Was NIE vergessen werden darf | **SOFORT** bei kritischer Erkenntnis |

### important-perceptions.md - Das "Institutional Memory"

Diese Datei ist eine **Barrikade** gegen wiederholte Fehler:

**✅ SCHREIBE SOFORT wenn:**
- Du 15+ Minuten an einem Problem debuggst
- Etwas kontraintuitiv funktioniert
- Eine Abhängigkeit nicht offensichtlich war
- Ein Pattern IMMER befolgt werden muss

**❌ SCHREIBE NICHT:**
- Offensichtliche Best Practices
- Iterationsspezifische Details (→ progress.txt)
- TODO-Items oder Feature-Ideen

---

## Tool-Nutzung

### Web-Recherche
Wenn du im Internet recherchieren musst (z.B. für Dokumentation, API-Referenzen, Fehlerbehebung), nutze **immer** das `web-search-prime_webSearchPrime` MCP-Tool. Dieses bietet bessere Suchergebnisse und ist für die Entwicklungsarbeit optimiert.
