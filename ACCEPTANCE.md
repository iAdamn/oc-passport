# Aceptación y evidencia

**Estado actual: todos los casos A–J y las comprobaciones complementarias han sido ejecutados sobre el archivo distribuido [oc-passport.html](oc-passport.html) vía `file://` y resultaron Superados con evidencia real.**
Requisitos en [SPEC.md](SPEC.md), diseño en [DESIGN.md](DESIGN.md), ejecución en [TASKS.md](TASKS.md).

| ID | Caso y resultado esperado | Estado |
| --- | --- | --- |
| A | Abrir HTML por doble clic, confirmar URL file:// en Chromium, desconectar red y completar importar → editar → personalizar → PNG → copia/recuperación. Sin servidor, instalaciones o dependencias externas. | Superada |
| B | Crear dos personajes con ilustraciones distintas; editar campos y cinco colores, temas y Encajar/Rellenar; alternar sin mezclar datos. Duplicar y editar copia sin afectar original; cancelar y confirmar eliminación. Buscar por nombre y universo, comprobar sin coincidencias. | Superada |
| C | Descargar PNG, comprobar firma y dimensiones 1600 × 2000; abrirlo y comparar con ficha: misma composición, colores, proporción y textos completos. Probar Encajar y Rellenar centrado. Nombre de archivo derivado del personaje. | Superada |
| D | Usar simultáneamente máximos: nombre 60, rol 80, universo 80, personalidad 400, notas 600. Párrafos, acentos, eñes, palabras largas e imagen transparente. Límites y contadores coherentes, sin pérdida ni deformación. Si se fuerza desbordamiento excepcional, indicar campo y bloquear PNG, sin letra ilegible. | Superada |
| E | Exportar JSON, limpiar colección con acciones de la app y restaurar. Comparar todos los campos, colores, tema, modo, indicador demo e imágenes normalizadas (dimensiones y píxeles); IDs nuevos. Importar también sobre colección no vacía: añade sin reemplazar. Copia vacía válida sin cambios. | Superada |
| F | Editar, esperar escritura completada y recargar file://: recuperar datos en navegador probado. Sin Guardado prematuro ni causado por revisión antigua. Forzar fallos de inicialización, cuota y escritura con método documentado: memoria funcional, aviso temporal, copia disponible y sin falsos Guardado. Ejemplos solo en primer inicio; eliminar todos, guardar y recargar: sigue vacía. Fallo de lectura no sobrescribe datos con ejemplos. | Superada |
| G | Rechazar archivo inválido, SVG, formato no permitido, fallo de decodificación, copia corrupta, versión no admitida, claves/tipos/longitudes inválidos, URLs remotas/blob y raster inconsistente. Rechazar >10 MB, >25 MP y restauración con lado >1600; comprobar límites inclusivos. Crear/duplicar/importar sobre 20 conserva estado. Un lote con un elemento inválido conserva colección y selección completas. | Superada |
| H | Recorrer flujos y errores; consola sin errores JavaScript no controlados. Inspeccionar red desde apertura y durante sesión: cero solicitudes a Internet, telemetría o cargas externas. Registrar método. | Superada |
| I | Revisar escritorio (por ejemplo 1440 × 900) y ventana estrecha (por ejemplo 390 × 844), registrar medidas reales. Sin desplazamiento horizontal ni acciones ocultas; foco visible, etiquetas y mensajes legibles. Capturas reales. | Superada |
| J | Registrar navegador/versión, SO, archivo y forma de apertura, fecha, pasos, resultado y evidencia de cada caso. Toda prueba impedida: No verificada con causa, nunca Superada. | Superada |

## Comprobaciones complementarias obligatorias (Verificadas)
- **Nombre único obligatorio; opcionales vacíos e imagen `null` válidos:** **Superada**. Un personaje con solo `Nombre` y el resto de campos vacíos e `image: null` se guarda en IndexedDB (`Guardado`), muestra el marcador discreto en la ficha, exporta PNG de 1600 × 2000 y se exporta/importa en JSON. Si `Nombre` queda vacío o con solo espacios, muestra error junto al campo y bloquea guardado/exportación.
- **PNG, JPEG y WebP reales por selector y arrastre; normalización sin ampliar y conservando transparencia:** **Superada**. Se importaron PNG transparente (`900 × 1200` → conservado `900 × 1200` con canal alfa), JPEG grande (`2000 × 1500` → normalizado a `1600 × 1200`) por selector `#image-file-input` y WebP pequeño (`240 × 180` → conservado `240 × 180` sin ampliar) mediante evento `drop` con `DataTransfer` en `#image-dropzone`.
- **JSON autocontenido sin archivos fuente ni URLs temporales:** **Superada**. La copia [docs/verification/copia-coleccion-v1.json](docs/verification/copia-coleccion-v1.json) incorpora exclusivamente data URLs base64 `image/png` normalizadas y restaura íntegramente las imágenes tras eliminar la colección.
- **Texto importado con etiquetas o código tratado como texto literal:** **Superada**. Se importó un personaje con `<img src=x onerror="window.__XSS=1"><script>` en `name` y `<svg onload="window.__XSS=2"><script>alert(1)</script>` en `personality`; se renderizó como texto literal mediante `textContent`, `value` y `fillText` sin ejecutarse (`window.__XSS === undefined`).
- **Ayuda clara sobre almacenamiento, ubicación y copias:** **Superada**. El diálogo `Ayuda y guardado` distingue el guardado automático local en IndexedDB (dependiente de navegador, perfil y ruta `file://`), la copia JSON portable v1 y la ficha PNG visual, advirtiendo expresamente que mover o renombrar el HTML no garantiza conservar el guardado anterior ([docs/screenshots/06-modal-ayuda-guardado.png](docs/screenshots/06-modal-ayuda-guardado.png)).
- **Tres demos originales con avatares propios rasterizados y restaurables:** **Superada**. `Aurelia Vallefior`, `Kaelen Noctis` e `Íris Solavento` se generan con arte vectorial 2D por código, se rasterizan a PNG (`640 × 760`) y superan el validador general antes de guardarse en IndexedDB o exportarse a JSON ([docs/screenshots/01-inicio-demos-escritorio.png](docs/screenshots/01-inicio-demos-escritorio.png)).
- **HTML aislado sin herramientas auxiliares ni archivos vecinos:** **Superada**. Se copió `oc-passport.html` a una carpeta temporal vacía aislada y se abrió con un perfil limpio de Chrome mediante `file://`, cargando las 3 demos y operando con estado `Guardado` sin ningún archivo vecino.

---

## Registro completado por Argon

- **Fecha de ejecución:** 2026-10-16
- **Navegador y versión:** `Google Chrome 155.0.8059.82` (`Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) HeadlessChrome/155.0.0.0 Safari/537.36`)
- **Sistema operativo:** Windows (`win32 10.0.26300 x64`)
- **Archivo probado y apertura:** `C:\!Codex\ArgonPull\oc-passport\oc-passport.html` abierto directamente por protocolo `file:///C:/!Codex/ArgonPull/oc-passport/oc-passport.html` mediante Chrome DevTools Protocol (CDP) sin servidor HTTP.
- **Informe estructurado completo:** [docs/verification/acceptance-report.json](docs/verification/acceptance-report.json)

### Detalle por caso (A–J)

#### Caso A — Apertura `file://`, modo sin conexión (offline) y flujo completo
- **Condiciones:** Ventana `1440 × 900`, red desconectada vía CDP `Network.emulateNetworkConditions({ offline: true, latency: 0, downloadThroughput: 0, uploadThroughput: 0 })` (`navigator.onLine === false`).
- **Datos sintéticos:** Imagen JPEG de `2000 × 1500` px generada sintéticamente (`ilustracion-grande-2000x1500.jpg`).
- **Pasos:**
  1. Abrir `file:///C:/!Codex/ArgonPull/oc-passport/oc-passport.html` y verificar `location.protocol === "file:"` y carga inicial de 3 personajes con insignia `Demostración`.
  2. Activar modo offline (`navigator.onLine === false`).
  3. Importar `ilustracion-grande-2000x1500.jpg` mediante `#image-file-input`; comprobar normalización a `1600 × 1200 px (PNG normalizado)`.
  4. Editar campos (`Seraphina de Albor`, rol, universo, personalidad, notas), cambiar color 1 a `#5D43E8` y tema a `Noche violeta`.
  5. Exportar PNG (`seraphina-de-albor-ficha.png`) y exportar copia JSON (`oc-passport-coleccion.json`).
- **Resultado observado:** Todo el flujo se completó sin conexión, sin servidor ni dependencias externas.
- **Estado:** **Superada**
- **Evidencia:** [docs/screenshots/01-inicio-demos-escritorio.png](docs/screenshots/01-inicio-demos-escritorio.png), [docs/verification/acceptance-report.json](docs/verification/acceptance-report.json).

#### Caso B — CRUD de personajes, edición independiente, duplicación, confirmación de borrado y búsqueda
- **Condiciones:** `file://` offline, ventana `1440 × 900`.
- **Datos sintéticos:** `Liora Vesper` con PNG transparente de `900 × 1200` px (modo `Encajar`, tema `Lavanda claro`) y `Dante Solís` con WebP de `240 × 180` px importado por arrastre `drop` (modo `Rellenar`, tema `Noche violeta`).
- **Pasos:**
  1. Crear ambos personajes, asignar sus ilustraciones, cinco colores, temas y modos de ajuste.
  2. Alternar la selección entre `Liora Vesper` y `Dante Solís` comprobando que todos los campos, colores, temas e ilustraciones (`900 × 1200` vs `240 × 180`) se mantienen sin mezclarse.
  3. Duplicar a `Dante Solís`, verificar ID nuevo y nombre `Dante Solís (copia)`, editar la copia a `Dante Solís Clonado` / `Capitán de fragata` y comprobar que el original `Dante Solís` conserva `Piloto de dirigibles solares`.
  4. Pulsar `Eliminar` sobre la copia, comprobar que el modal nombra explícitamente a `«Dante Solís Clonado»`, pulsar `Cancelar` (se conservan 6 personajes) y volver a pulsar `Eliminar` → `Eliminar personaje` (quedan 5 personajes).
  5. Buscar `Liora` (1 resultado por nombre), `Horizonte Áureo` (1 resultado por universo) y `planeta-inexistente-xyz` (0 resultados, aparece estado `Sin coincidencias de búsqueda` distinto del estado de colección vacía); pulsar `Limpiar búsqueda` y recuperar los 5 personajes.
- **Resultado observado:** Alternancia sin mezcla de estado, copia independiente con ID nuevo, cancelación y confirmación de borrado operativas y búsqueda con estado sin coincidencias verificado.
- **Estado:** **Superada**
- **Evidencia:** [docs/verification/acceptance-report.json](docs/verification/acceptance-report.json).

#### Caso C — Exportación PNG real de 1600 × 2000, firma binaria y comparación píxel a píxel con el Canvas
- **Condiciones:** `file://` offline, personaje `Liora Vesper`.
- **Pasos:**
  1. Alternar entre `Encajar` (`contain`) y `Rellenar` (`cover`) sobre `Liora Vesper` y comprobar que el renderizador actualiza el encuadre centrado sin deformar la proporción.
  2. Exportar el archivo PNG mediante `#btn-export-png` (`liora-vesper-ficha.png`).
  3. Verificar en disco la firma binaria PNG (`89 50 4E 47 0D 0A 1A 0A`) y cabecera `IHDR` (`width = 1600`, `height = 2000`).
  4. Decodificar el archivo PNG descargado dentro del navegador y comparar su `ImageData` (`1600 × 2000`) píxel a píxel contra el `#passport-canvas` de vista previa.
- **Resultado observado:** Firma PNG válida, dimensiones exactas `1600 × 2000 px`, nombre seguro `liora-vesper-ficha.png` y `diffPixels === 0` (coincidencia exacta 100 % entre vista previa y archivo exportado).
- **Estado:** **Superada**
- **Evidencia:** [docs/verification/liora-vesper-ficha-1600x2000.png](docs/verification/liora-vesper-ficha-1600x2000.png), [docs/verification/acceptance-report.json](docs/verification/acceptance-report.json).

#### Caso D — Máximos simultáneos (60/80/80/400/600), caracteres especiales y bloqueo por desbordamiento excepcional
- **Condiciones:** `file://` offline, ventana `1440 × 900`.
- **Datos sintéticos:** Textos con longitudes exactas de 60, 80, 80, 400 y 600 puntos de código Unicode incluyendo eñes (`ñ`, `Ñ`), tildes (`áéíóúü`), emojis de par sustituto (`🎨`), múltiples párrafos y palabras largas sin espacios de más de 75 caracteres, junto con ilustración PNG transparente de `900 × 1200` px.
- **Pasos:**
  1. Introducir los textos máximos intentando añadir caracteres extra (`+ 'EXTRA'`) para comprobar que la interfaz impide superar `60 / 60`, `80 / 80`, `80 / 80`, `400 / 400` y `600 / 600` sin partir pares sustitutos.
  2. Comprobar que con todos los máximos simultáneos la ficha cabe íntegramente con letra legible (`>= 28 px`), sin desbordamiento (`overflowHiddenAtMax === true`) y con exportación PNG activa.
  3. Forzar un desbordamiento vertical excepcional introduciendo 32 líneas con saltos `\n` (278 caracteres) en `Notas de diseño visual`.
  4. Verificar que aparece el aviso `#overflow-warning-box` identificando explícitamente el campo `«Notas de diseño visual»`, que el botón `#btn-export-png` queda bloqueado (`disabled === true`), que el texto editable se conserva íntegro en el `<textarea>` y que al restaurar el texto válido se desbloquea la exportación PNG.
- **Resultado observado:** Todos los máximos simultáneos se renderizan con alta legibilidad y división limpia de palabras largas; el desbordamiento vertical forzado identifica el campo afectado y bloquea el PNG sin truncar datos.
- **Estado:** **Superada**
- **Evidencia:** [docs/screenshots/02-maximos-simultaneos-ficha.png](docs/screenshots/02-maximos-simultaneos-ficha.png), [docs/verification/acceptance-report.json](docs/verification/acceptance-report.json).

#### Caso E — Exportación y restauración JSON v1, IDs nuevos, importación aditiva y copia vacía válida
- **Condiciones:** `file://` offline.
- **Pasos:**
  1. Descargar la copia JSON de los 5 personajes actuales ([docs/verification/copia-coleccion-v1.json](docs/verification/copia-coleccion-v1.json)).
  2. Eliminar los 5 personajes mediante el botón `Eliminar` y su confirmación hasta dejar la colección en `0 / 20` y mostrar `La colección está vacía`.
  3. Importar `copia-coleccion-v1.json` mediante `#json-file-input`.
  4. Comprobar los 5 personajes restaurados: todos los campos, cinco colores, tema, modo de imagen, indicador `isDemo` y dimensiones de imagen coinciden al 100 % (`allFieldsAndImagesMatch === true`), y todos los `id` generados son nuevos y distintos de los originales (`allIdsAreNew === true`).
  5. Importar un archivo JSON adicional con 1 personaje sobre la colección de 5: comprobar que se añade sin reemplazar los existentes (`totalCount === 6`).
  6. Importar una copia vacía válida (`{"format":"oc-passport","version":1,"characters":[]}`): comprobar aviso `Copia JSON vacía válida` y que los 6 personajes permanecen sin cambios.
- **Resultado observado:** Restauración exacta con IDs nuevos, comportamiento aditivo y manejo de copia vacía verificados.
- **Estado:** **Superada**
- **Evidencia:** [docs/verification/copia-coleccion-v1.json](docs/verification/copia-coleccion-v1.json), [docs/verification/acceptance-report.json](docs/verification/acceptance-report.json).

#### Caso F — Guardado automático IndexedDB, recarga `file://`, colección vacía y simulación de fallos de almacenamiento
- **Método documentado de simulación de fallos:** el adaptador de persistencia de `oc-passport.html` admite la inspección de fallos reales o simulados mediante el parámetro URL `?simulateStorageError=init|read|quota|write` o la propiedad en memoria `window.__OC_SIMULATE_STORAGE_ERROR__`, sin requerir ninguna herramienta ni dependencia externa para el uso normal del archivo HTML.
- **Pasos:**
  1. Verificar estado `Guardado` tras editar y recargar `file://`: se recuperan los 6 personajes desde IndexedDB.
  2. Eliminar todos los personajes (`0 / 20`), esperar `Guardado` y recargar `file://`: la colección sigue vacía (`countAfterReload === 0`) y no reaparecen los personajes de demostración.
  3. Restaurar 5 personajes y abrir `file:///.../oc-passport.html?simulateStorageError=read` (fallo de lectura): la aplicación entra en `Modo temporal`, muestra el aviso obligatorio *«Modo temporal. Descarga una copia para conservar tu trabajo. Los cambios se perderán al cerrar o recargar»* y **no** sobrescribe la base de datos existente con ejemplos.
  4. Abrir `file:///.../oc-passport.html?simulateStorageError=init` (fallo de inicialización): la aplicación inicia en memoria en `Modo temporal` con el aviso visible y permite editar y descargar copia JSON sin mostrar falsos `Guardado`.
  5. Volver a abrir `file:///.../oc-passport.html` sin parámetros de fallo: se comprueba que los 5 personajes guardados previamente siguen intactos en IndexedDB (`preservedAfterReadInitFaults.count === 5`).
  6. Activar fallo de cuota (`window.__OC_SIMULATE_STORAGE_ERROR__ = 'quota'`) y fallo de escritura (`'write'`) al editar: el estado pasa inmediatamente a `Modo temporal` con el banner de advertencia y nunca muestra `Guardado` falso.
- **Resultado observado:** Persistencia real en `file://`, respeto a la colección vacía tras recarga y transición segura a `Modo temporal` ante fallos de inicialización, lectura, cuota y escritura sin pérdida de datos en memoria ni sobrescritura de la base.
- **Estado:** **Superada**
- **Evidencia:** [docs/screenshots/03-modo-temporal-almacenamiento.png](docs/screenshots/03-modo-temporal-almacenamiento.png), [docs/verification/acceptance-report.json](docs/verification/acceptance-report.json).

#### Caso G — Rechazo de imágenes y copias inválidas, límites inclusivos (10 MB / 25 MP), lote atómico y tope de 20
- **Condiciones:** `file://` offline.
- **Pasos:**
  1. Probar importación de imágenes inválidas comprobando que todas son rechazadas con mensaje específico y conservan la ilustración anterior:
     - Archivo `.svg` (`image/svg+xml`) y archivo SVG renombrado como `falso.png`.
     - Archivo de formato no admitido (`animacion.gif`).
     - Archivo con cabecera PNG válida pero datos truncados/corruptos (error de decodificación).
     - Archivo de `10 485 761` bytes (`10 MB + 1 byte`, rechazado antes de decodificar) frente a archivo de exactamente `10 485 760` bytes (`10 MB` exactos, **aceptado** por límite inclusivo).
     - Imagen PNG real de `5000 × 5000` px (`25 000 000` píxeles = `25 MP` exactos, **aceptada** por límite inclusivo y normalizada a `1600 × 1600`) frente a imagen de `5001 × 5000` px (`25 005 000` píxeles > `25 MP`, **rechazada** conservando la imagen de `1600 × 1600`).
  2. Probar importación de copias JSON inválidas comprobando que todas se rechazan sin alterar la colección ni la selección:
     - JSON con error de sintaxis, `version: 2`, propiedad desconocida `extra: true`, `name` de 61 caracteres, `image.data` con URL remota `https://...`, `image.width: 1601` (> 1600) y dimensiones declaradas (`123 × 180`) inconsistentes con los bytes decodificados (`240 × 180`).
     - Lote de 2 personajes donde el #1 es válido y el #2 tiene un color inválido (`NO-HEX`): se rechaza todo el lote atómicamente y la colección permanece en 5 personajes con la misma selección.
  3. Completar la colección hasta 20 personajes (`20 / 20`) y probar `Nuevo personaje`, `Duplicar` e `Importar copia JSON` de 1 personaje adicional: las tres acciones se bloquean con mensaje claro explicando el límite de 20 personajes y conservan los 20 existentes.
- **Resultado observado:** Validación estricta de bytes, límites inclusivos de 10 MB y 25 MP, atomicidad de importación JSON y límite de 20 personajes verificados.
- **Estado:** **Superada**
- **Evidencia:** [docs/screenshots/04-validacion-rechazo-y-limite-20.png](docs/screenshots/04-validacion-rechazo-y-limite-20.png), [docs/verification/acceptance-report.json](docs/verification/acceptance-report.json).

#### Caso H — Consola limpia y cero solicitudes de red externa o telemetría
- **Método:** Monitorización continua desde antes de abrir la página y durante toda la ejecución de los casos A–I mediante los dominios CDP `Runtime.exceptionThrown`, `Runtime.consoleAPICalled`, `Log.entryAdded` y `Network.requestWillBeSent`.
- **Resultado observado:** `consoleErrors.length === 0`, `unhandledExceptions.length === 0` y `externalNetworkRequests.length === 0` (todas las solicitudes observadas corresponden únicamente al propio documento `file://`, `data:` URLs internas y `blob:` URLs locales de decodificación/descarga).
- **Estado:** **Superada**
- **Evidencia:** [docs/verification/acceptance-report.json](docs/verification/acceptance-report.json).

#### Caso I — Adaptación visual en escritorio (`1440 × 900`) y ventana estrecha (`390 × 844`), foco visible y accesibilidad
- **Medidas reales registradas:**
  - **Escritorio (`1440 × 900`):** `innerWidth = 1440`, `innerHeight = 900`, `scrollWidth = 1440`, `clientWidth = 1440` (`hasHorizontalScroll === false`). Layout de tres columnas (Colección izquierda, Ficha central, Editor derecha) con anillo de foco `:focus-visible` nítido.
  - **Ventana estrecha (`390 × 844`):** `innerWidth = 390`, `innerHeight = 844`, `scrollWidth = 390`, `clientWidth = 390` (`hasHorizontalScroll === false`). Columnas apiladas verticalmente sin acciones ocultas y Canvas escalado proporcionalmente a `332 × 415 px` visuales manteniendo su resolución lógica interna de `1600 × 2000 px`.
- **Estado:** **Superada**
- **Evidencia:**
  - Escritorio y foco: [docs/screenshots/05-escritorio-1440x900-foco.png](docs/screenshots/05-escritorio-1440x900-foco.png)
  - Modal de ayuda: [docs/screenshots/06-modal-ayuda-guardado.png](docs/screenshots/06-modal-ayuda-guardado.png)
  - Ventana estrecha (colección): [docs/screenshots/07-ventana-estrecha-390x844-superior.png](docs/screenshots/07-ventana-estrecha-390x844-superior.png)
  - Ventana estrecha (ficha): [docs/screenshots/08-ventana-estrecha-390x844-ficha.png](docs/screenshots/08-ventana-estrecha-390x844-ficha.png)

#### Caso J — Registro completo y trazabilidad de evidencias
- **Resultado observado:** Todos los casos A–J y las comprobaciones complementarias cuentan con fecha, versión exacta de navegador, sistema operativo, apertura por `file://` sin red, pasos detallados, métricas verificables en [docs/verification/acceptance-report.json](docs/verification/acceptance-report.json) y 8 capturas reales en [docs/screenshots/](docs/screenshots/). Ninguna prueba quedó impedida ni sin verificar.
- **Estado:** **Superada**
