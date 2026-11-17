# Plume Finder

**From a satellite methane detection to a complaint a resident can file.** Built at The Vakathon (July 2026).

Gas facilities across Texas, New Mexico and Oklahoma vent methane every day, and the people living next to them rarely know who is responsible or which regulator to tell. Plume Finder takes public satellite plume detections (Carbon Mapper / Tanager-1) and:

1. **Attributes** each plume to the most likely nearby facility and operator, with a confidence score.
2. **Routes** it to the right state regulator and the specific rule that applies (for example, New Mexico's 98% gas-capture rule versus Texas, which has no capture mandate).
3. **Drafts a complaint** residents can file, with an AI-drafted letter and a deterministic template fallback so the demo never depends on Wi-Fi.
4. **Lets neighbors corroborate** a plume with ground-truth reports and co-signs, which raises the attribution confidence.

Data: 47 real plumes across the Permian and Anadarko basins, with sources documented in [`data/SOURCES.md`](data/SOURCES.md). Texas operator names are labeled placeholders, because the state's public well layer has no operator field and we would not name a real company at an unverified location.

## Stack
FastAPI (Python) backend · React + TypeScript + Vite frontend · MapLibre + deck.gl map · Anthropic API

## My part
Team of 3 (Kishan Paschapur, Shiva Srinath, Shanay Verma). I built the frontend (map, plume resolve panel, report and co-sign UI, status tracker, three-state map with Oklahoma support) and the complaint-generation route with its offline fallback.

## Run it

```bash
# backend (from repo root)
pip3 install -r backend/requirements.txt
python3 -m uvicorn backend.main:app --port 8000

# frontend (second terminal)
cd frontend && npm install && npm run dev   # http://localhost:5173
```

Optional: `export ANTHROPIC_API_KEY=...` before starting the backend to get
AI-drafted complaint letters; without it a deterministic template letter is used
(demo never dead-ends on Wi-Fi).

More: [`docs/implementation_plan.md`](docs/implementation_plan.md) · [`docs/future_roadmap.md`](docs/future_roadmap.md)
