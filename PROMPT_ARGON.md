Actúa como Argon dentro de Antigravity y construye toda la v1 de OC Passport en una sesión autónoma.

Abre esta carpeta real:
C:\!Codex\ArgonPull\oc-passport

La preparación está completada. Todavía no existe una aplicación implementada ni pruebas de producto ejecutadas. Tu fase de implementación local está autorizada. No publiques, no crees repositorios remotos ni conectes servicios de pago.

Lee una vez al inicio AGENTS.md, README.md, SPEC.md, DESIGN.md, ACCEPTANCE.md, TASKS.md y HANDOFF.md. Después consulta las secciones necesarias sin releer todo antes de cada cambio. SPEC.md es la fuente principal del alcance. Inspecciona y conserva el trabajo útil y los cambios ajenos. El proyecto ya tiene Git local: no crees repositorios anidados.

Implementa oc-passport.html con HTML, CSS y JavaScript incluidos. Debe funcionar al abrirlo por doble clic con file:// en Chromium de escritorio, sin Internet, servidor, compilación ni instalaciones para el usuario final. No uses CDN, fuentes remotas, imports externos ni fetch de archivos vecinos. Las herramientas auxiliares de desarrollo y prueba no deben ser necesarias para ejecutar el HTML.

Completa el flujo importar ilustración → completar personaje → personalizar ficha → exportar PNG → guardar o recuperar colección. Implementa hasta 20 personajes, búsqueda y CRUD, nombre como único campo obligatorio, límites visibles, cinco colores, importación raster por selector y arrastre con validación y normalización, Encajar/Rellenar, dos temas y ficha de 1600 × 2000 mediante un único renderizador Canvas para vista previa y PNG. Resuelve máximos de texto, párrafos y palabras largas con legibilidad, sin recortar silenciosamente.

Implementa guardado automático IndexedDB con errores y modo temporal, Guardado solo tras completar la escritura de la revisión actual e indicador de inicialización separado para respetar una colección vacía. Incorpora tres demos originales con avatares vectoriales propios creados mediante código y rasterizados antes de guardar o copiar. Implementa copia JSON completa conforme al contrato v1 de SPEC.md e importación aditiva con IDs nuevos: valida todo y el límite final antes de modificar el estado.

Cuida la dirección visual de artbook, la interfaz en español, etiquetas, foco visible, ayuda y adaptación a escritorio y ventana estrecha. No añadas generación IA, APIs, backend, cuentas, telemetría, solicitudes de red ni funciones excluidas por SPEC.md.

Resuelve decisiones menores autónomamente. Pregunta solo ante un impedimento real que no puedas resolver dentro del alcance. Continúa hasta integrar, probar, corregir defectos y preparar la entrega.

Ejecuta todos los casos A–J y las comprobaciones complementarias de ACCEPTANCE.md sobre el HTML distribuido. Verifica file:// y funcionamiento offline, PNG abierto de 1600 × 2000, restauración JSON, persistencia y fallos de almacenamiento, límites, entradas inválidas, consola, red y diseño en dos tamaños. Registra navegador y versión, forma de apertura, pasos, resultados y evidencias reales. Si una prueba no puede ejecutarse, márcala No verificada y explica el motivo; nunca la declares superada por inferencia. Guarda capturas reales en docs/screenshots/. No fabriques evidencias ni incluyas datos personales.

Al finalizar actualiza README.md, ACCEPTANCE.md, TASKS.md y HANDOFF.md con estado real, uso, ayuda, resultados, limitaciones y vínculos a evidencias. Entrega localmente oc-passport.html autocontenido, documentación breve y evidencias verificables. En tu respuesta final indica la ruta de entrada, qué construiste, qué probaste realmente y cualquier limitación restante.
