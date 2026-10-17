# Traspaso y cierre de implementación (Argon)

## Ubicación y estado real
Carpeta del proyecto: **C:\!Codex\ArgonPull\oc-passport**

**Estado: v1 implementada, verificada en Chromium vía `file://` sin red y lista para entrega local.**
Entrada principal de la aplicación: [oc-passport.html](oc-passport.html).

## Inventario final entregado
- [oc-passport.html](oc-passport.html): aplicación v1 completa y autocontenida (HTML + CSS + JavaScript + tres personajes de demostración con avatares vectoriales propios creados por código y rasterizados a PNG). Funciona por doble clic (`file://`) sin servidor, compilación ni Internet.
- [AGENTS.md](AGENTS.md): instrucciones y autoridad del proyecto.
- [README.md](README.md): guía de uso, explicación de guardado automático frente a copia JSON portable y PNG, navegador probado y limitaciones.
- [SPEC.md](SPEC.md): especificación funcional v1 y contrato de copia JSON.
- [DESIGN.md](DESIGN.md): dirección visual e interacción.
- [ACCEPTANCE.md](ACCEPTANCE.md): matriz de aceptación A–J y comprobaciones complementarias con estado **Superada** y registro detallado de pruebas.
- [TASKS.md](TASKS.md): checklist de implementación y verificación completado.
- [PROMPT_ARGON.md](PROMPT_ARGON.md): prompt original de arranque.
- [docs/screenshots/](docs/screenshots/): 8 capturas reales tomadas desde Google Chrome `155.0.8059.82` abriendo `file:///C:/!Codex/ArgonPull/oc-passport/oc-passport.html`:
  - [01-inicio-demos-escritorio.png](docs/screenshots/01-inicio-demos-escritorio.png)
  - [02-maximos-simultaneos-ficha.png](docs/screenshots/02-maximos-simultaneos-ficha.png)
  - [03-modo-temporal-almacenamiento.png](docs/screenshots/03-modo-temporal-almacenamiento.png)
  - [04-validacion-rechazo-y-limite-20.png](docs/screenshots/04-validacion-rechazo-y-limite-20.png)
  - [05-escritorio-1440x900-foco.png](docs/screenshots/05-escritorio-1440x900-foco.png)
  - [06-modal-ayuda-guardado.png](docs/screenshots/06-modal-ayuda-guardado.png)
  - [07-ventana-estrecha-390x844-superior.png](docs/screenshots/07-ventana-estrecha-390x844-superior.png)
  - [08-ventana-estrecha-390x844-ficha.png](docs/screenshots/08-ventana-estrecha-390x844-ficha.png)
- [docs/verification/](docs/verification/): artefactos reproducibles generados durante las pruebas reales:
  - [acceptance-report.json](docs/verification/acceptance-report.json): informe técnico con las métricas y comprobaciones de los casos A–J.
  - [liora-vesper-ficha-1600x2000.png](docs/verification/liora-vesper-ficha-1600x2000.png): ficha PNG real de `1600 × 2000 px` exportada por la aplicación.
  - [copia-coleccion-v1.json](docs/verification/copia-coleccion-v1.json): copia JSON v1 autocontenida exportada y restaurada en las pruebas.

## Decisiones técnicas y correcciones aplicadas durante la sesión
1. **Renderizador único Canvas (`1600 × 2000 px`):** el elemento `#passport-canvas` mantiene una resolución lógica fija de `1600 × 2000` y se escala visualmente mediante CSS en la interfaz. La exportación PNG invoca exactamente la misma función `renderPassportCard`, garantizando coincidencia píxel a píxel (`diffPixels = 0`). Durante la verificación visual de las capturas se detectó y corrigió el orden de `ctx.clip()` en los bloques inferiores de texto para que el recorte se aplique al contenedor completo del bloque antes de dibujar la barra lateral de acento.
2. **Validación binaria y normalización raster:** se verifican las firmas mágicas de bytes (`PNG`, `JPEG`, `WebP`) además del tamaño (`<= 10 MB` inclusivo) antes de decodificar, y el conteo de píxeles (`<= 25 MP` inclusivo) tras decodificar. Se rechazan archivos SVG (incluso renombrados a `.png`), URLs remotas y archivos corruptos sin perder la ilustración previa.
3. **Persistencia IndexedDB y control de revisiones:** la base `oc-passport-v1-db` almacena el indicador `initialized` en el almacén `meta` y los personajes en `characters` dentro de una única transacción `readwrite` serializada. Solo se muestra `Guardado` cuando la transacción completada corresponde a `currentRevision`.
4. **Simulación de fallos de almacenamiento sin dependencias:** para verificar determinísticamente los fallos del Caso F sobre el propio HTML distribuido, el adaptador de IndexedDB permite inyectar fallos de apertura (`init`), lectura (`read`), cuota (`quota`) y escritura (`write`) mediante `?simulateStorageError=...` o `window.__OC_SIMULATE_STORAGE_ERROR__`, pasando de forma segura a **Modo temporal** sin sobrescribir datos previos.

## Limitaciones conocidas
- El guardado automático en IndexedDB bajo `file://` depende de las políticas del navegador Chromium, del perfil activo y de la ubicación del archivo; para conservar o mover colecciones de forma segura entre carpetas, navegadores o dispositivos debe utilizarse siempre **Descargar copia JSON**.
- La capacidad máxima está fijada en 20 personajes por colección conforme a [SPEC.md](SPEC.md).
