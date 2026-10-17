# Dirección visual e interacción

Aplicar dentro de [SPEC.md](SPEC.md). Comprobación en [ACCEPTANCE.md](ACCEPTANCE.md). Estado: diseño especificado, sin aplicación ni capturas de resultado.

## Dirección
Artbook interactivo y papelería digital de personajes: elegante, agradable y pulido. Violeta #6F5BFF para acciones, lila #9A7CFF para acentos, lavanda #DCCFFF y celeste #CFE9FF para superficies y detalles. Fuentes del sistema, títulos editoriales, cuerpo legible, bordes suaves y aire entre grupos. Evitar decoración que reste espacio al contenido.
Temas de ficha: lavanda claro (papel claro, tinta violeta oscura) y noche violeta (papel violeta oscuro, tinta clara). Mantener contraste de texto, controles y foco. Cinco colores personales como muestras y acentos controlados, sin volver ilegible texto esencial.

## Una composición
Canvas lógico fijo de 1600 × 2000. Margen de seguridad aproximado de 80 px. Cabecera con nombre, rol y universo; ventana protagonista de ilustración centrada; banda de cinco muestras; bloques inferiores de personalidad y notas visuales. Un campo opcional vacío puede liberar espacio, sin inventar contenido. Sin ilustración, marcador propio discreto.
La altura de imagen y distribución de texto se ajustan de forma determinista al contenido dentro de esta misma composición, para admitir máximos simultáneos. Los espaciados son guía, no motivo para recortar campos. Objetivo de legibilidad del PNG: cuerpo de al menos 28 px, nombre claramente mayor; verificar visualmente el resultado real. Si hay desbordamiento excepcional, identificar campo y bloquear PNG, conservando datos.
Encajar muestra toda la imagen y respeta transparencia sobre el tema. Rellenar recorta centrado. Un único renderizador comparte composición y ajuste entre vista previa y exportación.
Rotular ejemplos como Demostración en colección; no insinuar que sus avatares provienen de IA.

## Organización e interacción
Escritorio: colección compacta izquierda, ficha protagonista central y editor derecha si hay ancho. Editor agrupado en identidad, textos, ilustración, colores y apariencia. Copia JSON y ayuda localizables; PNG visible junto a ficha.
Ventana estrecha: apilar o reorganizar con orden comprensible, controles flexibles y Canvas escalado al contenedor. Todas las acciones esenciales accesibles sin desplazamiento horizontal.
Búsqueda por nombre o universo, selección reconocible. Duplicar crea copia independiente; eliminar confirma nombrando al personaje. Cambiar selección conserva ediciones. Cinco controles de color con etiquetas individuales y valor editable validado.

## Estados y mensajes
- Sin personajes: crear o importar; no volver a sembrar demos si se guardó vacío.
- Sin coincidencias: permitir limpiar búsqueda, distinguir de colección vacía.
- Sin ilustración: selector y zona de arrastre, formatos y límites visibles.
- Límite: explicar que hay 20 personajes y debe eliminar uno para añadir otro.
- Pendiente: indicar cambios por conservar; Guardado solo tras escritura de revisión actual.
- Fallo de almacenamiento: “Modo temporal. Descarga una copia para conservar tu trabajo. Los cambios se perderán al cerrar o recargar”.
- Archivo o copia inválidos: razón específica, estado anterior intacto.
- Texto que no cabe: campo afectado y acción para reducirlo; PNG bloqueado sin truncamiento.
- Nombre obligatorio y contadores: mensajes junto al campo.

Etiquetas y operación por teclado, foco visible. Anunciar estados relevantes de forma accesible sin interrumpir cada pulsación. Ayuda que distingue guardado de este navegador y ubicación, JSON portable y PNG visual. Detalles técnicos solo en ayuda. Sin controles de capacidades excluidas.
