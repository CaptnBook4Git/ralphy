# Ralphy Bugfixing Mode Prompt

Du befindest dich im **Bugfixing-Modus** für dieses Projekt.

## Deine Aufgabe

Du sollst Bugs aus der `bugs.json` Datei nacheinander reparieren. Die Bugs sind nach Priorität sortiert (critical > high > medium > low).

## WICHTIG: Bugfixing-Workflow

Für jeden Bug musst du:

1. **Den Bug verstehen**
   - Lies die Beschreibung sorgfältig
   - Analysiere die steps_to_reproduce
   - Suche nach dem root cause

2. **Den Bug fixen**
   - Identifiziere die betroffenen Dateien
   - Implementiere den Fix
   - Verwende bestehende Code-Patterns

3. **Verifizieren**
   - Reproduziere den Bug falls möglich
   - Teste, dass der Bug behoben ist
   - Führe Tests aus falls vorhanden
   - Prüfe auf Regressionen

4. **Dokumentieren**
   - Aktualisiere `bugs.json`:
     - Setze `"status": "resolved"`
     - Setze `"resolved": "YYYY-MM-DD"`
   - Füge einen Eintrag zu `progress.txt` hinzu

## Format für progress.txt (Bugfixing-Modus)

```
[YYYY-MM-DD HH:MM:SS] BUG-ID: Bug-Titel - [FIXED] Kurze Beschreibung des Fixes
```

Beispiel:
```
[2026-01-19 14:23:45] BUG-001: Login schlägt fehl bei falschem Passwort - [FIXED] Validierung der Passwort-Länge korrigiert
```

## Prioritäten-Reihenfolge

1. **Critical** (hochste Priorität)
2. **High**
3. **Medium**
4. **Low** (niedrigste Priorität)

## WICHTIG: Nur Bugs mit status="open"

Ignoriere Bugs, deren Status bereits auf "resolved" gesetzt ist.

## Beende die Session

Wenn alle Bugs mit status="open" behoben sind, solltest du:
1. Ein finales `<promise>COMPLETE</promise>` Tag ausgeben
2. Die Session beenden

## Code-Qualität

- Halte dich an bestehende Code-Patterns
- Füge Tests hinzu falls möglich
- Keine unnötigen Refactorings
- KISS-Prinzip (Keep It Simple, Stupid)

## WICHTIG: Du musst CODE SCHREIBEN und COMMITTEN

Dieser Modus ist für aktives Bugfixing, nicht nur für Analyse. Du musst:
- Code schreiben
- Fixes implementieren
- Commits erstellen
- Den Bug-Status aktualisieren

Viel Erfolg beim Bugfixing! 🐛🔨
