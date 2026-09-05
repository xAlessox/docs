# 🌙 Duerme Bebé

App web de **ruido blanco y canciones de cuna** para ayudar a dormir al bebé.

## Cómo usarla

Abre `app-bebe/index.html` en cualquier navegador (celular, tablet o computadora).
Es un solo archivo: no necesita instalación, servidor ni internet.

En el celular puedes agregarla a la pantalla de inicio (Compartir → "Añadir a
pantalla de inicio") y se comporta casi como una app nativa.

## Qué hace

- **8 sonidos ambientales**: lluvia, olas del mar, ruido blanco / rosa / marrón,
  ventilador, latido de mamá y "shhh" tipo útero.
- **4 canciones de cuna** con sonido de caja musical: Estrellita, Canción de cuna
  (Brahms), Noche de paz y Martinillo.
- Se puede mezclar **un sonido + una canción** a la vez.
- **Temporizador** (15/30/45/60 min) con desvanecido suave en los últimos 30 s,
  para que la música no se corte de golpe y despierte al bebé.
- **Modo noche**: pantalla en negro con la cuenta regresiva, para dejar el
  celular en el cuarto sin que ilumine.
- Mantiene la pantalla encendida mientras suena (donde el navegador lo permite)
  y recuerda el volumen y el temporizador elegidos.

## Cómo funciona por dentro

No hay archivos de audio: **todo se sintetiza en el momento** con la Web Audio
API del navegador. Por eso el archivo pesa ~23 KB y funciona sin conexión.

- **Los ruidos** salen de un búfer de ruido aleatorio de 8 segundos que se
  reproduce en bucle, pasado por filtros:
  - *blanco* = ruido crudo (todas las frecuencias por igual),
  - *rosa* = filtro de Paul Kellet (menos agudos, más natural al oído),
  - *marrón* = ruido integrado (muy grave, tipo cascada lejana).
- **Lluvia, olas, ventilador y "shhh"** son ese mismo ruido pasado por filtros
  paso-bajo/paso-banda, con un **LFO** (oscilador lento) moviendo el volumen o
  el brillo para que respire y no suene plano.
- **El latido** son dos golpes de onda senoidal (90 Hz → 38 Hz) programados a
  68 pulsaciones por minuto sobre un fondo de ruido marrón filtrado.
- **Las melodías** son osciladores (senoidal + triangular una octava arriba) con
  una envolvente de caída exponencial, pasados por una reverberación generada
  también con ruido que decae. Las notas se programan por adelantado con el
  reloj del audio (`ctx.currentTime`), que es mucho más preciso que `setTimeout`.

## Recomendaciones de uso

Pon el volumen bajo (que se oiga como una ducha suave, no más) y el celular
lejos de la cuna. El temporizador ayuda a que el sonido no se quede toda la
noche.
