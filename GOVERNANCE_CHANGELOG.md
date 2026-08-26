# Governance Changelog

Registro versionado de hitos de gobierno técnico aprobados para la organización `Gutierrez-Systems`.

## 2026-08-25 — Fase 1: Gobierno y protección de GitHub

### Contexto

La auditoría técnica detectó que las ramas principales de los repositorios revisados no estaban protegidas mediante enforcement real. Como remediación aprobada, la organización fue actualizada a GitHub Team y se habilitaron Rulesets para repositorios privados.

### Hito 1 — Piloto GS ContractOps

Se creó y activó el Ruleset organizacional:

`GS - Protección de main - Piloto ContractOps`

Aplicado únicamente a `GS-ContractOps`, con:

- rama objetivo: default branch (`main` actualmente);
- Pull Request obligatorio;
- aprobaciones requeridas: 0 mientras exista un único mantenedor;
- resolución obligatoria de conversaciones;
- status check obligatorio: `Lint, Typecheck y Build`;
- rama del PR actualizada frente a la principal;
- bloqueo de eliminación;
- bloqueo de force push;
- sin bypass configurado.

El repositorio pasó a reportar su rama principal como protegida.

### Hito 2 — Ruleset corporativo base

Se creó y activó el Ruleset organizacional:

`GS - Protección base de main - Corporativo`

Alcance:

- todos los repositorios de la organización;
- rama predeterminada de cada repositorio;
- Pull Request obligatorio;
- aprobaciones requeridas: 0 por ahora;
- resolución obligatoria de conversaciones;
- bloqueo de eliminación;
- bloqueo de force push;
- sin bypass configurado.

Este Ruleset no exige un status check global porque los repositorios actuales no comparten un pipeline CI homogéneo. Los checks obligatorios se definirán por repositorio en la fase de CI/DevSecOps.

### Principio de trazabilidad

Todo avance técnico o de gobierno aprobado debe quedar reflejado en:

1. Notion, como registro de contexto, decisión, estado y evidencia.
2. GitHub, como registro versionado de implementación, estándares o cambios técnicos.
3. Pull Requests y commits, cuando el avance implique cambios versionables.

La auditoría original se conserva como línea base histórica; las remediaciones posteriores se documentan sin sobrescribir el estado observado originalmente.

### Hito 3 — Inventario verificado de checks CI

Antes de crear Rulesets específicos de CI se verificaron los pipelines reales y sus últimas ejecuciones observadas en `main`.

Checks confirmados:

- `GS-ContractOps`: `Lint, Typecheck y Build` — ya exigido por su Ruleset específico.
- `gutierrez-systems-web`: `validar` — instala dependencias, ejecuta lint y build; ejecución observada exitosa.
- `gs-document-verification`: `Frontend` y `Backend` — ambos jobs observados exitosos.
- `eminser-cierre-nomina`: `validar` — lint, build y pruebas; ejecución observada exitosa.

Repositorios sin CI versionado observado durante la auditoría:

- `portal-prorroga-dosquebradas`;
- `gs-catalogo-interactivo`.

Decisión de implementación:

1. Mantener el Ruleset corporativo base para todos los repositorios.
2. Mantener el Ruleset específico existente de `GS-ContractOps`.
3. Crear un Ruleset específico de CI para `gutierrez-systems-web` y `eminser-cierre-nomina`, exigiendo `validar`.
4. Crear un Ruleset específico de CI para `gs-document-verification`, exigiendo `Frontend` y `Backend`.
5. Exigir que la rama del PR esté actualizada antes del merge en estos Rulesets específicos.
6. No exigir checks inexistentes a Portal, Catálogo u otros repositorios sin CI validado.

### Hito 4 — Activación de `GS - CI obligatorio - validar`

Se creó y activó el Ruleset organizacional:

`GS - CI obligatorio - validar`

Repositorios objetivo:

- `gutierrez-systems-web`;
- `eminser-cierre-nomina`.

Estado verificado mediante API de GitHub:

- enforcement: `active`;
- rama objetivo: default branch;
- check obligatorio: `validar`;
- política strict: activada, por lo que la rama del PR debe estar actualizada antes del merge;
- bypass: ninguno.

Hallazgo de verificación inicial:

El Ruleset conservaba una regla `deletion`, redundante con `GS - Protección base de main - Corporativo`. No introducía una brecha de seguridad, pero no coincidía con la separación de responsabilidades acordada.

Corrección aprobada y verificada:

- se retiró la regla redundante `deletion`;
- la API de GitHub confirma que el Ruleset específico contiene únicamente `required_status_checks`;
- el contexto obligatorio sigue siendo `validar`;
- `strict_required_status_checks_policy` permanece en `true`;
- bypass permanece vacío;
- enforcement permanece `active`.

Estado del hito: **cerrado y conforme al diseño corporativo**.

### Hito 5 — `GS - CI obligatorio - document verification`

Se creó y activó el Ruleset organizacional:

`GS - CI obligatorio - document verification`

Repositorio: `gs-document-verification`.

Verificación inicial:

- el segundo status check había quedado como `Bakend` en lugar de `Backend`;
- el criterio de ramas aparecía con `include: []`, sin rama objetivo efectiva.

Corrección aprobada y verificada por API:

- rama objetivo: `~DEFAULT_BRANCH`;
- checks obligatorios: `Frontend` y `Backend`;
- `strict_required_status_checks_policy`: `true`;
- `do_not_enforce_on_create`: `false`;
- bypass: ninguno;
- enforcement: `active`;
- el Ruleset específico contiene únicamente `required_status_checks`.

Estado del hito: **cerrado y conforme al diseño corporativo**.

### Hito 6 — Clasificación de `gs-catalogo-interactivo`

Se corrige explícitamente cualquier lectura que pudiera equiparar "sin CI versionado observado" con "repositorio secundario, histórico o inactivo".

`gs-catalogo-interactivo` es un **producto de Gutiérrez Systems en desarrollo activo**.

Evidencia y contexto:

- Notion lo documenta como producto digital en construcción, con FASE 1D en curso;
- repositorio dedicado: `Gutierrez-Systems/gs-catalogo-interactivo`;
- repositorio privado, no archivado y con `main` como rama predeterminada;
- la ausencia actual de CI versionado se interpreta como una **brecha de ingeniería activa a resolver**, no como una señal de inactividad.

Implicación para la remediación:

- `gs-catalogo-interactivo` pasa a prioridad alta para diseño e incorporación de CI compatible con su stack y flujo real de desarrollo;
- no se le impondrá un check genérico inventado;
- primero se auditarán su estructura, comandos, pruebas existentes y requisitos de reproducibilidad, y luego se definirá su pipeline específico.

Estado de clasificación: **producto activo confirmado**.

### Hito 7 — Clasificación de `GS-ContractOps`

Se deja explícito que `GS-ContractOps` es igualmente un **producto de Gutiérrez Systems en desarrollo activo**.

Implicaciones:

- su CI y Ruleset actuales gobiernan desarrollo activo y no mantenimiento pasivo;
- la existencia de controles técnicos sobre `main` no implica cierre ni madurez final del producto;
- las futuras decisiones de QA, seguridad, CI/CD y despliegue deben seguir su roadmap y estado real de evolución;
- `GS-ContractOps` y `gs-catalogo-interactivo` deben tratarse como productos activos prioritarios dentro del frente de ingeniería.

Estado de clasificación: **producto activo confirmado**.

### Hito 8 — Auditoría CI de `gs-catalogo-interactivo`

Se completó una auditoría técnica en modo solo lectura antes de diseñar cualquier gate obligatorio.

Hallazgos verificados:

- stack principal: Python;
- entorno histórico aprobado: Python 3.12.10;
- dependencia fijada: `PyMuPDF==1.28.2`;
- código: `src/extraccion_nativa/`;
- pruebas: suite `unittest` bajo `pruebas/`;
- el PDF real vive en `local/entrada/` y `local/` está excluido de Git;
- las pruebas dependientes del PDF real se omiten automáticamente cuando el archivo no existe;
- existen pruebas sintéticas que sí pueden ejecutarse en CI;
- no existe `.github/` ni workflow CI versionado en el producto;
- `main` está protegida por el Ruleset corporativo base, pero no existe Ruleset CI específico;
- el README actual es mínimo;
- `docs/fases/fase-1c-extraccion-nativa.md` conserva un estado documental anterior a la implementación y requiere corrección posterior.

Diseño CI v1 propuesto, pendiente de aprobación humana:

1. workflow `CI`;
2. check estable `Validar Python`;
3. Python 3.12.10;
4. instalación desde `requirements.txt`;
5. `python -m pip check`;
6. `python -m compileall -q src pruebas`;
7. `python -m unittest discover -s pruebas -p "test_*.py"`.

Exclusiones deliberadas de la primera iteración: Ruff, mypy, CodeQL, cobertura, OCR, IA y uso del PDF real en GitHub Actions. No se convertirán en gates hasta existir una configuración técnica validada.

Estado: **auditoría cerrada; diseño CI v1 pendiente de aprobación humana**.
