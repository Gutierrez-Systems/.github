# portal-prorroga-dosquebradas — Subhito C Ruleset CI obligatorio

## Estado previo verificado

- Repositorio: `Gutierrez-Systems/portal-prorroga-dosquebradas`.
- Ruleset corporativo base: `GS - Protección base de main - Corporativo` (ID `21484549`).
- Enforcement: `active`.
- Rama objetivo del Ruleset base: `~DEFAULT_BRANCH`.
- Reglas del Ruleset base: `deletion`, `non_fast_forward` y `pull_request` con resolución de conversaciones.
- Bypass: ninguno.

## Aprobación humana

Aprobado el Subhito C para crear un Ruleset CI específico del Portal.

## Configuración aprobada

Nombre:

`GS - CI obligatorio - portal prorroga`

Alcance:

- source: organización `Gutierrez-Systems`;
- repositorio: `portal-prorroga-dosquebradas`;
- target: branch;
- rama: `~DEFAULT_BRANCH`;
- enforcement: `Active`;
- bypass list: vacía.

Reglas:

- única regla específica: `required_status_checks`;
- status check requerido: `Validar Portal`;
- `strict_required_status_checks_policy`: `true`;
- `do_not_enforce_on_create`: `false`.

No duplicar en este Ruleset:

- restricción de borrado;
- non-fast-forward / force push;
- requisito de Pull Request;
- resolución de conversaciones.

Estas protecciones permanecen cubiertas por el Ruleset corporativo base ID `21484549`.

## Verificación posterior a la creación manual

Ruleset verificado mediante API:

- ID: `21534293`;
- nombre: `GS - CI obligatorio - portal prorroga`;
- source type: `Organization`;
- source: `Gutierrez-Systems`;
- target: `branch`;
- enforcement: `active`;
- condición de rama: `~DEFAULT_BRANCH`;
- reglas presentes: únicamente `required_status_checks`;
- check exacto: `Validar Portal`;
- `strict_required_status_checks_policy`: `true`;
- `do_not_enforce_on_create`: `false`;
- bypass actors: ninguno;
- `current_user_can_bypass`: `never`.

La lista efectiva del repositorio muestra ahora exactamente dos Rulesets aplicables:

1. `GS - CI obligatorio - portal prorroga` (ID `21534293`);
2. `GS - Protección base de main - Corporativo` (ID `21484549`).

No se detectaron reglas redundantes en el Ruleset CI específico.

## Estado

**Subhito C — CERRADO Y CONFORME.**

El Portal queda protegido por:

- Ruleset corporativo base para integridad de `main` y flujo por Pull Request;
- Ruleset CI específico que exige `Validar Portal` con rama actualizada antes del merge.
