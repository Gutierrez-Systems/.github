# portal-prorroga-dosquebradas — Auditoría CI

## Estado

Auditoría técnica en modo solo lectura completada. No se ha creado workflow CI ni Ruleset específico.

## Hallazgos verificados

- Repositorio: `Gutierrez-Systems/portal-prorroga-dosquebradas`.
- Visibilidad: privada.
- Rama predeterminada: `main`.
- `main` está protegida por el Ruleset corporativo base.
- No existe Ruleset CI específico efectivo.
- Stack: Next.js 16.3.0 + React 19.2.0 + TypeScript strict.
- Scripts disponibles: `dev`, `dev:turbo`, `setup:google`, `build`, `start`, `lint`.
- No existe script `test` ni suite de pruebas versionada observada.
- No se observó `.github/workflows/` versionado.
- No se observó lockfile en la raíz del repositorio.
- Varias dependencias/devDependencies usan `latest`: `googleapis`, `@types/node`, `@types/react`, `@types/react-dom`, `eslint`, `typescript`.
- El README indica instalación con `npm install`, por lo que el entorno actual no es determinista.
- `.env.example` usa marcadores para secretos; las credenciales Google/Supabase se consumen server-only.
- Los módulos de Google Drive y Supabase validan variables de entorno al ejecutar operaciones, no al importar el módulo, por lo que un build CI sin credenciales reales es viable en principio.

## Riesgo principal

No debe establecerse todavía un check obligatorio basado en una instalación no reproducible. Sin lockfile y con dependencias `latest`, dos ejecuciones pueden resolver versiones diferentes y producir resultados distintos.

## Secuencia de remediación propuesta

### Subhito A — Reproducibilidad

1. Sustituir dependencias `latest` por versiones concretas compatibles.
2. Generar y versionar `package-lock.json`.
3. Mantener `npm` como package manager actual.
4. Añadir un script `typecheck` explícito (`tsc --noEmit`) para no depender implícitamente de `next build`.

### Subhito B — CI v1

Una vez validada la reproducibilidad, crear workflow `CI` con un job estable, propuesto como `Validar Portal`, que ejecute:

1. `npm ci`;
2. `npm run lint`;
3. `npm run typecheck`;
4. `npm run build`.

No se proponen todavía tests como gate porque no existe suite de pruebas versionada. Tampoco se usarán secretos reales en CI.

### Subhito C — Ruleset

Solo después de que `Validar Portal` pase en PR y en `main`, crear un Ruleset específico que exija ese check y rama actualizada antes del merge.

## Estado de decisión

Auditoría cerrada. **Subhito A — Reproducibilidad pendiente de aprobación humana.**
