# Especificación v1 — fuente principal

Estado: especificación preparada; implementación y pruebas de producto pendientes. Instrucciones en [AGENTS.md](AGENTS.md), presentación en [DESIGN.md](DESIGN.md), comprobación en [ACCEPTANCE.md](ACCEPTANCE.md).

## Producto y distribución
OC Passport organiza personajes originales y compone fichas con ilustraciones del usuario. Flujo: importar ilustración → completar personaje → personalizar ficha → exportar PNG → guardar o recuperar colección.
Entrega: oc-passport.html con HTML, CSS, JavaScript y recursos de demostración incorporados. Debe funcionar por doble clic con URL file:// en Chromium de escritorio, sin Internet, servidor, compilación ni instalaciones para el usuario final.
Sin CDN, fuentes remotas, imports externos, librerías descargadas durante el uso ni fetch de archivos vecinos. Se permiten herramientas auxiliares de desarrollo y prueba; no serán necesarias para ejecutar el HTML. Entregar documentación breve y evidencias reales junto al HTML, con carpeta organizada para portafolio de GitHub.
El usuario aporta ilustraciones obtenidas previamente de cualquier herramienta. No hay IA, modelos, APIs, generación de imágenes, cuentas, backend ni botones que simulen esas capacidades. Sin telemetría o solicitudes de red. Excluidos chatbot, sincronización, autenticación, APK, instalador, marketplace e integraciones externas. Publicación, repositorios remotos y conexiones de pago quedan fuera del encargo local.

## Colección y campos
Máximo 20 personajes. Crear, seleccionar, editar, duplicar y eliminar con confirmación; buscar por nombre o universo. Crear, duplicar o importar por encima del límite muestra un mensaje claro y conserva lo existente. Duplicar conserva contenido con ID nuevo; las ediciones de la copia son independientes.
Nombre es el único campo obligatorio; validar que no quede vacío tras quitar espacios en extremos. No añadir campos obligatorios adicionales. Es válido guardar un personaje sin ilustración, con un estado vacío en su ficha.

| Campo | Tipo | Máximo visible |
| --- | --- | --- |
| Nombre | Texto | 60 caracteres |
| Título o rol | Texto | 80 caracteres |
| Universo | Texto | 80 caracteres |
| Personalidad | Texto con párrafos | 400 caracteres |
| Notas de diseño visual | Texto con párrafos | 600 caracteres |
| Colores | Cinco colores editables | Exactamente cinco valores #RRGGBB |

Mostrar límites y contadores, impedir excesos sin truncar datos importados. Usar igual cómputo en interfaz e importación; decisión v1: puntos de código Unicode (Array.from(texto).length), sin cortar pares sustitutos. Campos opcionales vacíos son válidos.

## Ilustraciones
Una ilustración principal por personaje, mediante selector y arrastrar/soltar. Solo PNG, JPEG y WebP raster válidos. Máximo inicial de 10 MB (10 × 1024 × 1024 bytes) y 25 megapíxeles (25 000 000 píxeles), límites inclusivos. Comprobar tamaño antes de decodificar y dimensiones tras decodificar, antes de normalizar. No confiar solo en extensión o MIME declarado: comprobar formato real y decodificación.
Rechazar SVG del usuario, URLs remotas, imágenes inválidas y otros formatos. Mensajes útiles para formato, tamaño, dimensiones y errores de decodificación. Conservar la imagen anterior ante error.
Normalizar lado mayor a máximo 1600 px conservando proporción y transparencia; no ampliar imágenes menores. La representación interna y portable es raster normalizado; PNG es la elección v1 para serializar sin perder transparencia. Liberar recursos temporales cuando corresponda.
Encajar predeterminado: ilustración completa centrada sin deformación. Rellenar: ocupa ventana mediante recorte centrado sin deformación. No hay editor libre de recorte.

## Ficha y PNG
Vista previa inmediata de ficha vertical de 1600 × 2000 px, escalada visualmente para caber en interfaz. Una sola composición bien terminada y dos temas: lavanda claro y noche violeta. Campos, cinco colores, tema e ilustración se reflejan al editar o seleccionar personaje.
Un único renderizador Canvas produce la ficha previa y el PNG. Exportar PNG real de exactamente 1600 × 2000, con nombre de archivo seguro derivado del personaje y extensión .png.
Resolver párrafos, saltos de línea, acentos, eñes, palabras largas y los máximos de todos los campos simultáneamente. Mantener tamaños legibles; dividir palabras largas si hace falta. Nunca recortar texto silenciosamente ni reducir letra hasta volverla ilegible. Si excepcionalmente no cabe, identificar el campo y bloquear PNG hasta corregirlo. Conservar texto editable y permitir copia JSON para no perder trabajo. Véase DESIGN.

## Guardado y primer inicio
Guardado automático mediante IndexedDB cuando el navegador lo permita. Gestionar errores de apertura/inicialización, cuota y escritura. Si falla, continuar en memoria y explicar que debe descargar una copia para conservar el trabajo. En modo temporal advertir que cerrar o recargar pierde los cambios de la sesión.
Mostrar Guardado solo después de completar la transacción correspondiente al estado actual. Al editar, marcar pendiente; una escritura antigua no puede marcar como guardada una revisión nueva. Serializar escrituras o controlar revisiones.
Persistir colección e indicador de inicialización separado en una transacción coherente. Distinguir base sin inicializar, colección vacía guardada y fallo de lectura; un fallo no autoriza sobrescribir datos con ejemplos.
Primer inicio: tres personajes originales identificados como demostración, con pequeños avatares vectoriales propios creados mediante código e incorporados al HTML. Rasterizarlos a PNG o WebP antes de guardarlos como imágenes de personajes o incluirlos en JSON. Restaurarlos bajo la misma validación raster general.
Una colección vacía guardada es válida. Los ejemplos eliminados no reaparecen con persistencia disponible. Una sesión temporal puede comenzar con ejemplos y debe advertir de la pérdida al recargar.
Explicar en ayuda que el guardado depende de navegador, perfil y ubicación del archivo; no prometer que mover el HTML conserva datos. La interfaz comunica acciones prácticas; IndexedDB y detalles técnicos pertenecen a la ayuda.

## Copia JSON versionada
Descargar e importar copia completa con imágenes normalizadas incorporadas, campos, cinco colores, tema, modo de imagen e indicador de demostración. Nunca rutas de disco, blob URLs, enlaces remotos ni referencias temporales.

Contrato v1 decidido para validación inequívoca:
- Raíz con campos permitidos: format = "oc-passport", version = 1, characters = array.
- Cada personaje: id (cadena no vacía hasta 128 caracteres), name, role, universe, personality, visualNotes (cadenas con límites anteriores), colors (array de cinco #RRGGBB), theme ("lavender" o "violet-night"), imageFit ("contain" o "cover"), isDemo (booleano), image (null u objeto siguiente).
- image: mime ("image/png", "image/jpeg" o "image/webp"), data (data URL base64 de ese formato), width y height (enteros positivos). Comprobar bytes reales, decodificación, concordancia de MIME y dimensiones, lado mayor ≤1600 y límites raster anteriores. No confiar en metadatos declarados.
- Rechazar versiones no admitidas, propiedades desconocidas, campos de esquema ausentes, tipos incorrectos y valores fuera del contrato. Los campos opcionales de interfaz se serializan como cadena vacía; image puede ser null. No usar coerciones ni mezclar propiedades importadas con objetos de aplicación.

Los IDs del archivo describen la copia; al importar generar IDs nuevos y únicos en la colección. No restaurar desde la copia el indicador de inicialización del navegador.
Importación aditiva y atómica: leer y validar todo en estructura aislada, decodificar todas las imágenes y comprobar límite final de 20 antes de añadir el lote completo. Ante error, colección, selección y datos previos permanecen intactos. No reemplazar personajes existentes silenciosamente. Copia vacía válida: no altera lo existente. Exportar copia no depende de IndexedDB.
Textos mediante APIs de texto y Canvas, nunca HTML ejecutable. No ejecutar contenido importado.

## Interfaz y entrega
Todo en español. Controles etiquetados, foco visible de teclado, estados vacíos, validaciones y mensajes comprensibles. Escritorio: colección compacta, ficha protagonista y editor organizado. Ventana estrecha: reorganizar sin ocultar acciones esenciales ni causar desplazamiento horizontal.
Paleta base: violeta #6F5BFF, lila #9A7CFF, lavanda #DCCFFF y celeste #CFE9FF. Fuentes del sistema, jerarquía editorial, bordes suaves y espaciado generoso.
Argon implementará, integrará, probará y corregirá toda la v1. Registrará resultados observados en ACCEPTANCE y capturas reales en docs/screenshots/. Pruebas impedidas: No verificada. Actualizar README, TASKS y HANDOFF al terminar.
