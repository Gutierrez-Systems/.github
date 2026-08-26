# portal-prorroga-dosquebradas — Auditoría CI

## Estado

Auditoría técnica en modo solo lectura completada. No se ha creado todavía workflow CI permanente ni Ruleset específico.

## Hallazgos verificados

- Repositorio: `Gutierrez-Systems/portal-prorroga-dosquebradas`.
- Visibilidad: privada.
- Rama predeterminada: `main`.
- `main` está protegida por el Ruleset corporativo base.
- No existe Ruleset CI específico efectivo.
- Stack: Next.js 16.3.0 + React 19.2.0 + TypeScript strict.
- Scripts originales: `dev`, `dev:turbo`, `setup:google`, `build`, `start`, `lint`.
- No existe script `test` ni suite de pruebas versionada observada.
- No existía `.github/workflows/` versionado antes de la remediación.
- No existía lockfile en la raíz antes de la remediación.
- Varias dependencias/devDependencies usaban `latest`: `googleapis`, `@types/node`, `@types/react`, `@types/react-dom`, `eslint`, `typescript`.
- `.env.example` usa marcadores para secretos; las credenciales Google/Supabase se consumen server-only.
- Los módulos de Google Drive y Supabase validan variables de entorno al ejecutar operaciones, no al importar el módulo, por lo que el build puede validarse sin credenciales reales.

## Subhito A — Reproducibilidad

Aprobación humana recibida e implementación realizada en la rama:

`chore/reproducibilidad-ci-20260825`

### Cambios permanentes preparados

- `package.json`:
  - `googleapis`: `176.0.0`;
  - `@types/node`: `26.3.0`;
  - `@types/react`: `19.2.18`;
  - `@types/react-dom`: `19.2.5`;
  - `eslint`: `9.39.5`;
  - `typescript`: `6.0.3`;
  - nuevo script `typecheck`: `tsc --noEmit`.
- `package-lock.json` generado y versionado con lockfileVersion 3.
- npm se mantiene como package manager.

### Validación técnica

GitHub Actions se utilizó temporalmente para generar y validar el lockfile sin introducir secretos reales.

Run de validación aislada: `32922999519`.

Resultados:

- generación de `package-lock.json`: success;
- `npm ci`: success;
- `npm run typecheck`: success;
- `npm run build`: success;
- npm reportó 0 vulnerabilidades en la resolución/instalación observada.

El workflow auxiliar fue retirado después de la validación. El diff final contra `main` contiene únicamente:

- `package.json`;
- `package-lock.json`.

### Hallazgo separado — ESLint

Durante una validación previa se confirmó que `npm run lint` falla antes de analizar código porque el repositorio no contiene `eslint.config.(js|mjs|cjs)` y ESLint 9 exige configuración flat.

Este hallazgo **no se corrige dentro del Subhito A** porque requiere una decisión/aprobación separada antes de construir el CI v1.

### Estado del Pull Request

PR #9: `chore: hacer reproducibles las dependencias`.

Verificación realizada:

- estado: `open`;
- draft: `false`;
- mergeable: `true`;
- base: `main`;
- head: `chore/reproducibilidad-ci-20260825`;
- head SHA: `16566ebd355c9a5fcca09be9ce2310718f5387d9`;
- archivos cambiados: únicamente `package.json` y `package-lock.json`;
- alcance: conforme con el Subhito A aprobado;
- merge: pendiente de control humano.

Estado del Subhito A: **implementado, validado y abierto en PR #9; pendiente de merge humano**.

## Siguiente secuencia

### Subhito B1 — Configuración ESLint

Pendiente de aprobación posterior: incorporar una configuración ESLint compatible con Next.js 16 / ESLint 9 y validar `npm run lint`.

### Subhito B2 — CI v1

Después de cerrar B1, crear workflow `CI` con job estable `Validar Portal`:

1. `npm ci`;
2. `npm run lint`;
3. `npm run typecheck`;
4. `npm run build`.

### Subhito C — Ruleset

Solo después de que `Validar Portal` pase en PR y en `main`, crear un Ruleset específico que exija ese check y rama actualizada antes del merge.
