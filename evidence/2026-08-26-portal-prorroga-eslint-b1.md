# portal-prorroga-dosquebradas — Subhito B1 ESLint

## Aprobación y alcance

Subhito B1 aprobado humanamente para incorporar una configuración ESLint compatible con Next.js 16 / ESLint 9, sin modificar lógica funcional, CI permanente, secretos ni Rulesets.

## Implementación

- Rama: `chore/eslint-config-next16-20260826`.
- Archivo permanente añadido: `eslint.config.mjs`.
- Configuración basada en `eslint-config-next/core-web-vitals` y `eslint-config-next/typescript`.
- Se añadieron ignores explícitos para artefactos generados (`.next/**`, `out/**`, `build/**`, `next-env.d.ts`).

## Validación

Se utilizó un workflow temporal únicamente para ejecutar la validación real en GitHub Actions.

Run: `32933533886`.

Pasos observados:

- `npm ci`: success;
- `npm run lint`: success.

El workflow temporal fue retirado después de validar.

Comparación final contra `main`:

- únicamente `eslint.config.mjs`;
- 14 líneas añadidas;
- ningún cambio funcional adicional.

## Pull Request

PR #10: `chore: configurar eslint para Next.js 16`.

- estado al abrir: `open`;
- base: `main`;
- head: `chore/eslint-config-next16-20260826`;
- head SHA: `31b9492b148adcf19b0f2bf2502d2ba7e309f82d`;
- changed files: 1;
- archivo: `eslint.config.mjs`.

Estado del Subhito B1: **implementado, validado y abierto en PR #10; pendiente de merge humano**.

Siguiente paso solo después del merge y verificación en `main`: **Subhito B2 — CI v1 (`Validar Portal`)**.
