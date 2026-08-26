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

Hallazgo de verificación:

El Ruleset conserva además una regla `deletion`, redundante con `GS - Protección base de main - Corporativo`. No introduce una brecha de seguridad, pero debe retirarse del Ruleset específico para mantener la separación de responsabilidades acordada: protección base en el Ruleset corporativo y CI en los Rulesets específicos.

Estado del hito: **activo y funcional, pendiente de limpieza de la regla redundante `deletion` antes de cierre definitivo**.
