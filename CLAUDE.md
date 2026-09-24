# Guardián del Tiempo (Toastmasters Medellín)

Single-file dashboard (`index.html`, no build) for the session's Cronometrador. Spanish UI.

## Behavior
- Table follows the agenda order. Columns: Descripción, Socio, Rol, Mínimo, Máximo, Cronómetro, Real, Estado.
- "Cargar agenda (PDF)" builds all rows from the published agenda PDF (pdf.js 3.11.174 from cdnjs, parsed by header column positions INICIO/FIN/SOCIO).
- Roles with Ficha 03 ranges (min+max): Discurso Preparado (max-2:00), Evaluación and Reporte (max-1:00), Table Topic (1:00-2:00 default). Other roles (Toastmaster, Topicsmaster, Presidencia, Presentación de rol, Otro) have only a max = agenda time.
- Stopwatch per row (timestamp-based, survives throttled tabs). Signals: green at min, yellow at midpoint, red at max, shown on the button, row, and large speaker card with emoji and text. Speaker mode uses a fixed `100dvh` overlay instead of the Fullscreen API so it works on mobile Safari; it includes an on-screen close control and requests a screen wake lock when supported.
- Independent session clock tracks actual start against the scheduled start (taken from the PDF when available). The planned agenda position and finish time use row maxima; omitted rows are removed from the plan.
- Topicsmaster and Table Topic rows share one 20-minute block clock. It starts with the first such row and continues across speaker changes. Starting a non-topic row pauses it. The planned agenda counts the whole block once as 20 minutes.
- "+ Añadir participante" inserts a Table Topic right after the last Table Topic / Topicsmaster row.
- Report: can be generated from completed rows at any point. It groups interventions by person, retains each role, and shows a duration bar and range. Share as PNG through the Web Share API when supported or download it for WhatsApp.
- State (rows, title, skipped rows, session/block clocks, running stopwatch) persists in localStorage key `guardian-del-tiempo`.
- Light and dark theme via tokens (`prefers-color-scheme`).

## Gotchas
- pdf.js splits words at accents and the PDF uses decomposed accents: normalize NFC, sort fragments by `Math.round(y)`, classify ignoring whitespace.
- Agenda durations are H:MM:SS.
- Unconfirmed with the Toastmaster: min ranges, spelling Jonhatan/Johnatan.

## Deploy
- Static hosting (GitHub Pages recommended). No server, PDF is read in the browser.
- The old Claude artifact copy is not maintained; `index.html` is the source of truth.
