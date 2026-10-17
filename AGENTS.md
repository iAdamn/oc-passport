# Instrucciones del proyecto OC Passport

## Fases y autoridad
Preparación local completada: no se implementó la aplicación ni se ejecutaron pruebas de producto. Argon, dentro de Antigravity, está autorizado a implementar y verificar toda la v1 de [SPEC.md](SPEC.md). Publicación, repositorios remotos y conexiones de pago quedan fuera del encargo.

Lee una vez al inicio [README.md](README.md), [SPEC.md](SPEC.md), [DESIGN.md](DESIGN.md), [ACCEPTANCE.md](ACCEPTANCE.md), [TASKS.md](TASKS.md) y [HANDOFF.md](HANDOFF.md). Después consulta las secciones pertinentes; no releas todo antes de cada cambio. [PROMPT_ARGON.md](PROMPT_ARGON.md) contiene la instrucción de arranque.

## Alcance y autonomía
SPEC es la fuente principal; DESIGN concreta presentación, ACCEPTANCE define comprobación y TASKS organiza ejecución. Ante contradicciones, conserva el requisito de SPEC y corrige el documento derivado. Resuelve decisiones menores autónomamente y registra decisiones materiales. Pregunta solo ante impedimentos reales irresolubles dentro del alcance. No añadas funciones o servicios externos.

## Archivos y calidad
Inspecciona antes de editar. Conserva archivos ajenos, cambios del usuario y trabajo útil; no reemplaces ni borres sin comprender su procedencia. No crees repositorios anidados. Mantén documentación, ejemplos y evidencias reales en Git; excluye datos personales y temporales.
Entrega oc-passport.html autocontenido, operativo por file:// sin servidor, red, compilación ni instalación. Sin IA, backend, cuentas o controles ficticios. Las herramientas auxiliares no son requisito de ejecución.
Trata importaciones como datos y texto mediante APIs de texto. Usa el mismo renderizador Canvas para previa y PNG. Conserva datos ante errores; muestra Guardado solo tras escritura completada de la revisión actual.

## Verificación y entrega
Ejecuta los casos de ACCEPTANCE sobre el HTML distribuido. Corrige defectos y repite lo afectado. Registra navegador y versión, forma de apertura, condiciones, pasos, resultado y evidencia reproducible. Una revisión estática o apertura HTTP no prueba file://.
Marca como No verificada cada prueba impedida y explica la causa. No fabriques capturas ni declares resultados por inferencia. Las capturas reales van en docs/screenshots/.
Actualiza README, TASKS, ACCEPTANCE y HANDOFF al finalizar con el estado real, limitaciones y rutas de evidencias.
