# Guardián del Tiempo (Toastmasters Medellín)

Single-file dashboard (`index.html`, no build) for the session's Cronometrador. Spanish UI.

## Behavior
- Table follows the agenda order. Columns: Descripción, Socio, Rol, Mínimo, Máximo, Cronómetro, Real, Estado.
- "Cargar agenda (PDF)" builds all rows from the published agenda PDF (pdf.js 3.11.174 from cdnjs, parsed by header column positions INICIO/FIN/SOCIO).
- Roles with Ficha 03 ranges (min+max): Discurso Preparado (max-2:00), Evaluación and Reporte (max-1:00), Table Topic (1:00-2:00 default). Other roles (Toastmaster, Topicsmaster, Presidencia, Presentación de rol, Otro) have only a max = agenda time.
- Stopwatch per row (timestamp-based, survives throttled tabs). Signals: green at min, yellow at midpoint, red at max, always with text.
- "+ Añadir participante" inserts a Table Topic right after the last Table Topic / Topicsmaster row.
- Report: groups by En rango / Por debajo / Por encima. Duplicate socios get the description appended.
- State (rows, title, running stopwatch) persists in localStorage key `guardian-del-tiempo`.
- Light and dark theme via tokens (`prefers-color-scheme`).

## Gotchas
- pdf.js splits words at accents and the PDF uses decomposed accents: normalize NFC, sort fragments by `Math.round(y)`, classify ignoring whitespace.
- Agenda durations are H:MM:SS.
- Unconfirmed with the Toastmaster: min ranges, spelling Jonhatan/Johnatan.

## Deploy
- Static hosting (GitHub Pages recommended). No server, PDF is read in the browser.
- The old Claude artifact copy is not maintained; `index.html` is the source of truth.
