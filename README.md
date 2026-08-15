# Pinta y Puzles

App de pintar y hacer puzles para iPad, pensada para una niña de 4 años y
compatible con iOS 12 (iPad mini 2).

## Qué hace

**Pintar** — 10 colores, 3 grosores, goma, 8 sellos (emoji), deshacer y
"papel nuevo" (hay que mantener pulsado 1 segundo, con un anillo que se va
llenando, para que no lo borre todo sin querer). El dibujo se guarda solo y
sigue ahí al volver a abrir la app.

**Parejas** — juego de memoria al estilo de la tablet de Ikea: 8 dibujos de
carta (rayas, lunares, damero, estrella, corazón, triángulos, diana, zigzag)
con dorso rojo e interrogación. Tres niveles: 3, 6 u 8 parejas. Las cartas
giran con animación, las iguales se quedan abiertas y las distintas se cierran
solas al cabo de un segundo.

**Puzles** — 8 gatitos generados por código: naranja de cerca, gris sentado,
blanco dormido bajo la luna, negro con lazo, atigrado con un ovillo, uno
asomando de una caja, uno mirando una mariposa en el jardín y otro sentado en
la ventana de noche. Las piezas se arrastran con el dedo, encajan
solas al acercarlas y suena un tono. El tablero muestra la imagen en marca de
agua como ayuda.

Progresa por niveles: cada puzle completado sube uno y arranca el siguiente
con otro dibujo al azar, cada vez con más piezas.

| Niveles | Rejilla | Piezas |
|---------|---------|--------|
| 1–2     | 2×2     | 4      |
| 3–4     | 3×2     | 6      |
| 5–6     | 3×3     | 9      |
| 7–8     | 4×3     | 12     |
| 9–10    | 4×4     | 16     |
| 11–12   | 5×4     | 20     |

A partir del 12 el contador sigue subiendo y se mantiene en 20 piezas. El
nivel se guarda en el iPad, así que continúa donde lo dejó. La medalla de la
barra inferior muestra el nivel y los puntos, el avance.

Para volver al nivel 1: **mantener pulsada la medalla 1,5 segundos**. Es
deliberadamente largo para que no lo haga ella sin querer.

El botón de la miniatura abre el selector por si quiere cambiar de dibujo sin
cambiar de nivel.

## Instalación recomendada

1. Sube los tres archivos (`index.html`, `sw.js`, `icon-180.png`) a un
   repositorio de GitHub y activa GitHub Pages. Hace falta HTTPS: el service
   worker no funciona por HTTP.
2. Abre la URL en Safari en el iPad, una sola vez.
3. Compartir → **Añadir a pantalla de inicio**.
4. Desde ese momento la app arranca a pantalla completa y funciona sin
   conexión y sin ningún servidor encendido: el service worker ya guardó todo
   en el iPad.

Si cambias `index.html`, sube el número de versión en `sw.js` (`pinta-v4` →
`pinta-v5`) o el iPad seguirá sirviendo la copia antigua.

## Antes de dársela

Ajustes → Accesibilidad → Acceso Guiado → activar. Con la app abierta, triple
clic en el botón de inicio y queda bloqueada dentro de la app.

## Notas técnicas

Un solo archivo, sin dependencias ni red. Escrito para el motor de iOS 12: sin
encadenamiento opcional, sin `gap` de flexbox, sin `clamp()`, sin eventos de
puntero (solo eventos táctiles). El lienzo se dibuja a `devicePixelRatio`
limitado a 2. Las piezas del puzle se pre-renderizan una vez a su propio
lienzo y el acierto del toque se calcula por canal alfa, para que arrastrar
vaya fluido en el A7.
