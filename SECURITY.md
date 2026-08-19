# Política de Seguridad

Gutierrez Systems aplica seguridad por defecto en código, configuración y documentación.

## Reporte de vulnerabilidades

No publiques credenciales, datos personales ni detalles explotables en Issues públicos. Cuando exista un canal privado formal, debe utilizarse para reportes sensibles.

## Secretos y configuración

No deben versionarse contraseñas, tokens, claves privadas, service-role keys, archivos `.env` reales, credenciales de proveedores ni dumps con información personal o empresarial.

Los archivos de ejemplo deben usar únicamente nombres de variables y valores ficticios seguros.

## Datos

Para desarrollo y pruebas se prefieren datos sintéticos o anonimizados. El uso de datos reales requiere necesidad justificada, autorización y controles adecuados.

## Producción

Los secretos deben obtenerse desde el proveedor de ejecución y los permisos deben seguir el principio de mínimo privilegio.

## Incidentes

Ante una exposición accidental de credenciales: revocar o rotar, evaluar impacto, retirar el secreto del estado actual, limpiar historial cuando sea necesario y registrar la acción correctiva en documentación interna.

Las políticas específicas de cada repositorio prevalecen cuando establecen controles más estrictos.
