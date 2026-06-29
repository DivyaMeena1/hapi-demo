# HAPI FHIR server test (Docker)

Minimal stack: **HAPI + Postgres + demo page**. No Matchbox.

- `$extract` — definition-based (metadata in Questionnaire, no FML per form)
- `$transform` — shared StructureMap resources on HAPI (not per form)
- `$translate` — ConceptMap on HAPI
- FHIR REST + Patient search

## Start

```powershell
cd C:\Users\meena\Desktop\Projects\exp\HapiServerTest
docker compose up -d
```

- **Team demo:** http://localhost:8091
- **HAPI direct:** http://localhost:8090/fhir/metadata
- **Swagger:** http://localhost:8090/fhir/swagger-ui/index.html

First boot can take 1–2 minutes.

## Stop

```powershell
docker compose down
```

Remove Matchbox if it was left running:

```powershell
docker rm -f okrx-matchbox
```

## Layout

- `docker-compose.yml` — HAPI, Postgres, nginx demo
- `config/application.yaml` — Clinical Reasoning enabled
- `demo/index.html` — interactive demo
- `samples/` — Questionnaire, ConceptMap, etc.
