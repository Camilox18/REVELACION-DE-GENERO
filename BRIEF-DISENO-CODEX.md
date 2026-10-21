# Revelación de género — Brief de diseño y desarrollo

## Objetivo
Construir una invitación web de revelación de género, responsive y ligera, con estética editorial artesanal/collage. Prioridad: dirección gráfica cuidada y una animación de sobre sencilla, estable y fácil de probar en móvil y escritorio.

## Dirección visual aprobada
- Estilo: editorial, hecho a mano, vintage sutil, papel y collage analógico. Limpio; no recargado ni demasiado infantil.
- Paleta:
  - Blanco humo: `#F4F4F2` — fondo general/base clara.
  - Marfil cálido: `#F3ECD2` — hojas, recortes y papel del sobre.
  - Borgoña: `#60151A` — titulares, círculo de fecha, detalles lineales y botones.
- Texturas: fibras visibles de papel, grano fotográfico sutil, bordes rasgados, pliegues, sombras suaves y cinta de papel. Evitar filtros fuertes o texturas que reduzcan la legibilidad.
- Tipografía de titulares: lettering digital orgánico y manuscrito, con trazo redondeado y expresivo pero no excesivamente bold. Usar una fuente web real; no rasterizar titulares ni dibujar letras en una imagen. Referencias visuales aportadas: lettering de “Farm to Table” y “Organic Cultura”.
- Textos secundarios: serif mono / máquina de escribir o una tipografía con carácter editorial, siempre legible.
- Ilustración: casi ninguna. Como máximo, una pequeña planta prensada/seca junto al sobre, como elemento real de collage. El único recurso gráfico dibujado añadido puede ser un círculo irregular alrededor de la fecha. No llenar la página de iconos.

## Composición principal
- El sobre ya aparece abierto en el primer estado; no animar una apertura completa desde cero.
- La cabecera de la hoja sobresale del sobre desde el inicio y muestra parte del titular.
- Dos fotos originales de los futuros padres cuando eran niños aparecen como fotografías separadas, superpuestas al sobre como collage. No poner las fotos dentro de la hoja.
- Añadir cinta de papel, bordes de foto tipo impresión antigua, pequeñas sombras naturales y tratamiento tonal cohesivo.
- No añadir una tarjeta flotante extra con el texto “¿niño o niña?”; se descartó porque no aporta.

## Fotos originales: reglas importantes
- Utilizar las dos fotos originales facilitadas por el usuario.
- No regenerar las caras con IA ni cambiar facciones, expresiones, peinados o ropa.
- Se permiten retoques muy moderados de exposición, balance de blancos, contraste, reducción ligera de ruido y grano/pátina uniforme para integrar las fotos en el collage.
- Recortar manteniendo las caras y detalles relevantes; los dos retratos deben conservar su aspecto auténtico.
- Preparar archivos separados y referenciarlos desde `assets/` con nombres claros. Si todavía no están guardadas en el proyecto, dejar marcadores/placeholders y solicitar las originales; no inventar fotos.

## Texto de la invitación
Titular principal en minúsculas:
“revelación de nuestro hije”

Mensaje:
“Estás invitado a un momento muy especial para los papás y nos encantaría que nos acompañes.”

Cierre:
“¡te esperamos!”

Evitar frases genéricas como “una historia está por comenzar”. Mantener el tono personal y natural.

## Evento
- Fecha: sábado 7 de noviembre de 2026.
- Hora: 4:30 p. m.
- Lugar: El Polo 703, Santiago de Surco, Lima, Perú.
- Mes y fecha deben tratarse como datos del evento, no como fecha actual.

Enlace de Google Maps (búsqueda de dirección; verificar el pin exacto antes del lanzamiento):
`https://www.google.com/maps/search/?api=1&query=El+Polo+703%2C+Santiago+de+Surco%2C+Lima%2C+Per%C3%BA`

Confirmación por WhatsApp:
- Crear botón con texto claro “Confirmar por WhatsApp”.
- El teléfono receptor está pendiente; no inventar número. Centralizarlo en una constante fácil de configurar, por ejemplo `WHATSAPP_PHONE`.
- Cuando se agregue el número en formato internacional sin `+` ni espacios, crear URL `https://wa.me/NUMERO?text=...` con un mensaje de confirmación preescrito.

## Sección de equipos
Los equipos deben estar impresos/compuestos en la parte inferior de la MISMA hoja de invitación, dentro de la zona del sobre. No deben parecer tarjetas separadas flotando por delante del sobre.
- “team niña” — “Traes pañales.”
- “team niño” — “Traes pañitos húmedos.”

Usar recortes de papel discretos si ayudan al collage, pero mantenerlos visualmente integrados a la carta.

## Animación / interacción del scroll
Objetivo: la hoja tiene suficiente altura para revelar todo el contenido en varios tramos. Mientras el usuario baja, el sobre se desplaza hacia abajo y el papel sube, descubriendo gradualmente titular, mensaje, equipos y finalmente la zona inferior de datos/acciones.

Importante evitar fallos observados en el primer prototipo:
- El sobre no debe quedarse inmóvil cuando la hoja sigue moviéndose.
- El papel no debe recortarse desde abajo ni desaparecer detrás de una capa por error.
- Evitar clipping accidental de titulares, textos, fotos o tarjetas.
- No crear transformaciones incompatibles entre capas que provoquen que el papel salga del marco.
- Usar una sola progresión de scroll normalizada para coordinar el movimiento de la carta y el sobre.
- Dar a la carta altura real suficiente; ajustar espacio de scroll al contenido en lugar de limitarlo a un viewport fijo.
- Probar `overflow`, `z-index`, `transform-origin`, `position: sticky` y alturas en navegadores reales.
- Respetar `prefers-reduced-motion`: en ese caso, dejar la invitación visible sin depender de animaciones.
- La animación debe ser suave, discreta y vinculada al scroll. No añadir auto-scroll ni movimientos bruscos.

## Responsive y accesibilidad
- Diseñar primero para móvil, también revisar escritorio.
- Sin desbordamiento horizontal; textos y botones cómodos al tacto.
- Contraste suficiente en borgoña sobre papel claro.
- Los enlaces deben abrir WhatsApp/Maps de manera funcional y segura.
- Si se usa `position: sticky`, comprobar Safari/iOS y navegadores Chromium.
- Las fuentes externas son aceptables, pero la página debe seguir siendo legible si no cargan.

## Jerarquía prevista de la experiencia
1. Portada: sobre ya abierto, cabecera de papel saliendo, titular y fotos superpuestas.
2. Al bajar: la hoja asciende y revela el mensaje de invitación.
3. Sigue la carta: aparecen `team niña` y `team niño` integrados en el papel.
4. Final: datos del evento y botones de confirmar por WhatsApp y abrir Google Maps.
5. Cierre breve: “¡te esperamos!” si no queda mejor en la parte media de la carta.

## Antes de publicar
- Reemplazar placeholders con las dos fotografías originales.
- Añadir el número correcto de WhatsApp.
- Verificar el pin exacto de Google Maps.
- Comprobar la fecha/hora y todos los textos con el usuario.
- Probar scroll en móvil y escritorio, incluyendo el final de la carta.
- Revisar rendimiento, carga de imágenes, accesibilidad básica y enlaces.
- Publicar con GitHub Pages cuando la versión final esté aprobada.

## Principios para Codex
- No rehacer la dirección de arte ni introducir elementos nuevos sin consultarlo.
- Priorizar edición incremental y código claro, sin frameworks innecesarios para una invitación estática.
- Mantener datos del evento y teléfono en una sección/configuración fácil de editar.
- No sustituir los retratos por versiones generadas por IA.
- Resolver primero la estructura y el movimiento; después pulir espaciados y detalles.
