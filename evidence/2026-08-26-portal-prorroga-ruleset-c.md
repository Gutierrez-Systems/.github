# portal-prorroga-dosquebradas — Subhito C Ruleset CI obligatorio

## Estado previo verificado

- Repositorio: `Gutierrez-Systems/portal-prorroga-dosquebradas`.
- Ruleset efectivo actual: `GS - Protección base de main - Corporativo` (ID `21484549`).
- Enforcement: `active`.
- Rama objetivo del Ruleset base: `~DEFAULT_BRANCH`.
- Reglas del Ruleset base: `deletion`, `non_fast_forward` y `pull_request` con resolución de conversaciones.
- Bypass: ninguno.
- No existe todavía un Ruleset CI específico para este repositorio.

## Aprobación humana

Aprobado el Subhito C para crear un Ruleset CI específico del Portal.

## Configuración exacta aprobada

Nombre propuesto:

`GS - CI obligatorio - portal prorroga`

Alcance:

- source: organización `Gutierrez-Systems`;
- repositorio seleccionado únicamente: `portal-prorroga-dosquebradas`;
- target: branch;
- rama: `~DEFAULT_BRANCH`;
- enforcement: `Active`;
- bypass list: vacía.

Reglas:

- **única regla específica**: `required_status_checks`;
- status check requerido: `Validar Portal`;
- source/integration: `Any source` cuando la UI lo solicite;
- `strict_required_status_checks_policy`: `true` (Require branches to be up to date before merging = ON);
- `do_not_enforce_on_create`: `false`.

No duplicar en este Ruleset:

- restricción de borrado;
- non-fast-forward / force push;
- requisito de Pull Request;
- resolución de conversaciones.

Estas protecciones ya están cubiertas por el Ruleset corporativo base ID `21484549`.

## Estado

**Aprobado y pendiente de creación/activación manual en GitHub.**

La integración disponible permite verificar Rulesets mediante API, pero no crear/modificar Rulesets de organización. Después de la activación manual debe verificarse por API el ID, enforcement, alcance, check exacto y ausencia de reglas redundantes antes de cerrar el Subhito C.
