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
