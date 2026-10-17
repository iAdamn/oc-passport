# OC Passport

**Estado: v1 implementada y verificada localmente (`OC-Passport.exe` y `oc-passport.html`).**

Aplicación local autocontenida en español para organizar hasta **20 personajes originales** y componer fichas editoriales de **1600 × 2000 px** a partir de ilustraciones raster aportadas por el usuario.

## Entrada y ejecución

- **Aplicación de escritorio (`.exe`):** [OC-Passport.exe](OC-Passport.exe) — haz doble clic en `OC-Passport.exe` para abrir OC Passport como una ventana de aplicación de escritorio dedicada (sin pestañas ni barra de direcciones del navegador), con perfil local persistente en `%LOCALAPPDATA%\OCPassport\UserData` y el recurso `oc-passport.html` integrado dentro del propio ejecutable.
- **Archivo HTML autónomo (`file://`):** [oc-passport.html](oc-passport.html) — también puedes abrirlo directamente por doble clic mediante `file://` en un navegador Chromium de escritorio (como Google Chrome o Microsoft Edge).
- **Sin dependencias externas:** no requiere conexión a Internet, servidor local, compilación, instalaciones ni archivos vecinos.

## Flujo de uso

1. **Importar ilustración:** selecciona o arrastra una imagen raster propia en formato **PNG, JPEG o WebP** (máximo **10 MB** y **25 megapíxeles**). La aplicación verifica los bytes reales del formato, comprueba dimensiones y normaliza el lado mayor a un máximo de **1600 px** conservando proporción y transparencia (sin ampliar imágenes menores).
2. **Completar personaje:** rellena el **Nombre** (único campo obligatorio, hasta 60 caracteres) y los campos opcionales: **Título o rol** (80), **Universo** (80), **Personalidad** (400, admite párrafos) y **Notas de diseño visual** (600, admite párrafos). Todos los límites usan conteo por puntos de código Unicode (`Array.from(texto).length`).
3. **Personalizar ficha:** elige el modo de ajuste de la ilustración (**Encajar** completa centrada o **Rellenar** con recorte centrado), el tema visual de la lámina (**Lavanda claro** o **Noche violeta**) y los **cinco colores personales** (`#RRGGBB`) mediante selector visual o código hexadecimal validado.
4. **Exportar PNG:** pulsa **Exportar PNG (1600 × 2000)** para descargar la ficha en alta resolución generada por el mismo renderizador Canvas que muestra la vista previa en vivo.
5. **Guardar o recuperar la colección:** utiliza **Descargar copia JSON** e **Importar copia JSON** para respaldar, trasladar o restaurar tus personajes con sus ilustraciones incorporadas.

## Guardado automático, copias JSON y exportación PNG

- **Guardado automático en este navegador (IndexedDB):** OC Passport guarda automáticamente cada revisión válida en el almacenamiento local del navegador y muestra el estado **Guardado** únicamente cuando la transacción de la revisión actual ha concluido. En el primer inicio sobre una base sin inicializar, carga tres personajes originales identificados como **Demostración** (`Aurelia Vallefior`, `Kaelen Noctis` e `Íris Solavento`) con avatares vectoriales propios creados por código y rasterizados a PNG. Si eliminas todos los personajes, la colección vacía se respeta al recargar.
- **Dependencia de navegador y ubicación:** el guardado automático depende del navegador, del perfil de usuario y de la ruta `file://` desde la que se abre el archivo. Mover o renombrar `oc-passport.html`, usar ventanas privadas o cambiar de navegador no garantiza recuperar automáticamente los datos previos.
- **Modo temporal ante fallos de almacenamiento:** si IndexedDB está bloqueado, falla al iniciar/leer o supera la cuota disponible (`QuotaExceededError`), la aplicación continúa funcionando en memoria, activa el aviso de **Modo temporal** e invita a descargar una copia JSON antes de cerrar o recargar.
- **Copia JSON portable (`oc-passport` v1):** archivo `.json` autocontenido con todos los campos, cinco colores, ajustes e imágenes normalizadas en base64. La importación valida todo el lote antes de modificar el estado y es **aditiva**: añade los personajes importados con identificadores nuevos sin sobrescribir los existentes, respetando el límite total de 20 personajes.
- **Ficha PNG (1600 × 2000 px):** imagen final de presentación para portafolio o impresión; no sustituye a la copia JSON editable.

## Verificación y evidencias

- **Navegador probado:** Google Chrome `155.0.8059.82` (64 bits) sobre Windows (`win32 10.0.26300 x64`), abierto mediante `file:///C:/!Codex/ArgonPull/oc-passport/oc-passport.html` y verificado sin conexión (`offline`).
- **Resultados detallados:** consulta [ACCEPTANCE.md](ACCEPTANCE.md) y el informe estructurado [docs/verification/acceptance-report.json](docs/verification/acceptance-report.json).
- **Capturas reales de verificación:** disponibles en [docs/screenshots/](docs/screenshots/).
- **Artefactos verificados (PNG 1600 × 2000 y copia JSON v1):** disponibles en [docs/verification/](docs/verification/).

## Alcance y limitaciones de la v1

- La v1 no incluye generación de imágenes por IA, modelos, APIs, cuentas de usuario, sincronización en la nube ni backend.
- El límite de colección es de 20 personajes simultáneos para mantener fluidez y portabilidad de las copias JSON con ilustraciones raster incorporadas.
- Si un campo de texto contiene una cantidad extraordinaria de saltos de línea que impida mostrar todo el texto en el lienzo de 1600 × 2000 px con el tamaño mínimo legible (28 px), la aplicación identifica el campo afectado y bloquea temporalmente la exportación PNG sin recortar el texto ni impedir la copia JSON.

## Documentos del proyecto

- [AGENTS.md](AGENTS.md): instrucciones y autoridad del proyecto.
- [SPEC.md](SPEC.md): especificación funcional y contrato de datos v1.
- [DESIGN.md](DESIGN.md): dirección visual, composición e interacción.
- [ACCEPTANCE.md](ACCEPTANCE.md): casos de aceptación A–J, comprobaciones complementarias y registro real de pruebas.
- [TASKS.md](TASKS.md): lista de tareas completadas.
- [HANDOFF.md](HANDOFF.md): estado final de entrega e inventario.
