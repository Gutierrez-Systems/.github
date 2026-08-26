# gs-catalogo-interactivo — CI v1

## Estado

CI v1 incorporado a `main` y verificado.

## Evidencia

- Producto: `Gutierrez-Systems/gs-catalogo-interactivo`
- PR de implementación: #8 — `ci: agregar validación Python v1`
- Estado PR: merged
- Merge commit: `bcbbd76050187aff746c98775e9ff56229c6082c`
- Workflow en `main`: `.github/workflows/ci.yml`
- Workflow run sobre `main`: `32920650357`
- Evento: `push`
- Job/check: `Validar Python`
- Resultado: `success`

## Validaciones ejecutadas

- Python 3.12.10
- instalación desde `requirements.txt`
- `python -m pip check`
- `python -m compileall -q src pruebas`
- `python -m unittest discover -s pruebas -p "test_*.py"`

## Seguridad y datos

El PDF fuente real continúa fuera de Git y no es requerido por GitHub Actions.

## Siguiente control

El workflow ya existe y pasa en `main`, por lo que el repositorio está técnicamente listo para crear un Ruleset específico que exija el check `Validar Python`, sujeto a aprobación humana y verificación posterior por API.
