# HAPI FHIR server test (Docker)

Hybrid stack: **HAPI** for `$extract`, `$translate`, Patient search, and persistence; **Matchbox** for `$transform` only.

| Operation | Engine | Endpoint |
|-----------|--------|----------|
| `$extract` | HAPI | `POST /fhir/QuestionnaireResponse/$extract` (definition-based, flat Questionnaire) |
| `$transform` | Matchbox | `POST /matchbox/fhir/StructureMap/$transform` (FML map in `demo/legacy-patient-normalize.fml`) |
| `$translate` | HAPI | `GET /fhir/ConceptMap/$translate` |
| Patient search / storage | HAPI | `GET /fhir/Patient?...` |

**Requires** Clinical Reasoning enabled in HAPI (`config/application.yaml`). After config changes: `docker compose down && docker compose up -d` (first boot 1–2 min).

## Start

```powershell
cd C:\Users\meena\Desktop\Projects\exp\HapiServerTest
docker compose up -d
```

- **Team demo:** http://localhost:8091
- **HAPI direct:** http://localhost:8090/fhir/metadata
- **Matchbox (via proxy):** http://localhost:8091/matchbox/fhir/metadata
- **Swagger:** http://localhost:8090/fhir/swagger-ui/index.html

First boot can take 1–2 minutes (HAPI + Matchbox).

## Stop

```powershell
docker compose down
```

## Layout

- `docker-compose.yml` — HAPI, Matchbox, Postgres, nginx demo
- `config/application.yaml` — Clinical Reasoning enabled on HAPI
- `config/matchbox-application.yaml` — Matchbox `onlyOneEngine` + `httpReadOnly: false` (required for `$transform`)
- `demo/index.html` — interactive demo (engine split)
- `demo/legacy-patient-normalize.fml` — FML map for Matchbox `$transform`
- `demo/structuremap-legacy-patient-normalize.json` — equivalent StructureMap JSON (reference)
- `samples/` — flat Questionnaire, ConceptMap, StructureMap examples
