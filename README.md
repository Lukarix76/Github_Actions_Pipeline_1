# Simulador Mundial 2026

[![QA](https://github.com/Lukarix76/Github_Actions_Pipeline_1/actions/workflows/qa.yml/badge.svg)](https://github.com/Lukarix76/Github_Actions_Pipeline_1/actions/workflows/qa.yml)
[![Allure Report](https://img.shields.io/badge/Allure-Report-5A2D82)](https://lukarix76.github.io/Github_Actions_Pipeline_1/)

App FastAPI con frontend estático y suite QA automatizada con `pytest`, Playwright y Allure.

## Qué hace GitHub Actions

El repo tiene dos workflows:

- `QA`: instala dependencias, corre tests API, levanta la app, ejecuta el smoke frontend y genera `allure-results`, `allure-report`, `coverage.xml` y `uvicorn.log`.
- `Publish Allure Report`: publica el HTML de Allure en GitHub Pages cuando `QA` termina bien sobre un `push` a la rama por defecto.

Archivos:

- [.github/workflows/qa.yml](./.github/workflows/qa.yml)
- [.github/workflows/allure-pages.yml](./.github/workflows/allure-pages.yml)

## Cómo ver el reporte

1. En GitHub, entrar a `Settings > Pages`.
2. En `Source`, seleccionar `GitHub Actions`.
3. Hacer un `push` a la rama por defecto.
4. Esperar a que terminen `QA` y `Publish Allure Report`.

URL esperada del sitio:

```text
https://lukarix76.github.io/Github_Actions_Pipeline_1/
```

## Ejecución local

Instalación:

```bash
pip install -r requirements.txt
python -m playwright install chromium
```

Tests API:

```bash
pytest tests -m "not frontend" -v
```

Smoke frontend:

```bash
python -m uvicorn main:app --host 127.0.0.1 --port 8000
APP_URL=http://127.0.0.1:8000 pytest tests/test_frontend_smoke.py -v
```

Allure local:

```bash
pytest tests -v --alluredir=allure-results
allure generate allure-results --clean -o allure-report
```

## Documentación QA

- [QA.md](./QA.md)
- [docs/qa-simulator-run.md](./docs/qa-simulator-run.md)
- [PROMPT_RTC_QA.md](./PROMPT_RTC_QA.md)

## Enlaces

- Repositorio: https://github.com/Lukarix76/Github_Actions_Pipeline_1
- Reporte Allure publicado: https://lukarix76.github.io/Github_Actions_Pipeline_1/
