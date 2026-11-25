# Instrucciones para Claude: proyecto "Bloqueados: Horda Mutante"

Este repositorio es el portafolio de Saúl y contiene un juego de zombis para iPhone/web hecho en un solo archivo HTML (canvas + JavaScript, sin dependencias de compilación). Habla siempre en **español (México)** con el dueño del repo.

## Las dos versiones del juego (MUY IMPORTANTE)

| Carpeta | Qué es | ¿Se modifica? |
|---|---|---|
| `juego-base/` | **Versión base congelada** (v1.9.1-base). Es la que se convertirá en app para la **App Store**. | **NO. Nunca la modifiques** salvo que el dueño lo pida de forma explícita diciendo "versión base" o "App Store". |
| `juego/` | **Versión de la comunidad.** Es la que está publicada en la web y se va mejorando con las ideas de los comentarios de TikTok ("Tú decides"). | Sí. Aquí van todos los cambios normales. |

Si el dueño pide un cambio sin decir a cuál versión, **aplícalo solo en `juego/`**.

## Cómo hacer un cambio en la versión de la comunidad

1. Todo el juego está en `juego/index.html` (HTML + CSS + JS en un solo archivo). La fuente está en `juego/fonts/`, PeerJS (modo en línea) en `juego/peerjs.min.js`.
2. **Sube el número de versión** en `<meta name="game-version" content="X.Y.Z">` de `juego/index.html`. El juego compara ese número al abrir y se recarga solo en los teléfonos de los jugadores. Si no lo subes, la gente seguirá viendo la versión vieja.
3. **Prueba antes de subir** con Playwright (Chromium ya viene instalado): abre `juego/index.html`, juega unos minutos simulados y revisa que no haya errores en la consola. Revisa también cómo se ve en iPhone **vertical y horizontal** (por ejemplo 390×844 y 844×390, y un teléfono chico como 375×667).
4. Si el cambio toca el modo en línea, prueba con dos páginas conectadas (el juego acepta `?peer=host:puerto` para usar un servidor PeerJS local de pruebas).
5. Actualiza la sección "Cómo jugar" (`#help` en el HTML) si el cambio agrega armas, enemigos o mecánicas.
6. Haz commit con un mensaje en español que explique qué idea de la comunidad se agregó (si se sabe, el usuario de TikTok que la propuso).

## Datos útiles del código

- Partida en solitario y en línea comparten la lógica: el anfitrión corre `update()`; los invitados reciben "fotos" del estado (`buildSnap` / `applySnap`). Si agregas algo nuevo que se vea en pantalla (enemigos, proyectiles, objetos), **inclúyelo en la foto** para que los invitados también lo vean.
- Los efectos visuales/sonoros pasan por `fx(nombre, ...)` para que se repliquen a los invitados.
- El guardado (monedas, mejoras, récords) está en `localStorage` con la clave `bloqueados_save_v1`; no rompas su formato (agrega campos con valores por defecto).
- El video promocional de TikTok se generó con un script de Playwright que avanza el juego cuadro por cuadro; si el dueño pide otro video, se puede repetir la técnica.

## Lo que NO hay que hacer

- No modificar `juego-base/`.
- No borrar el progreso de los jugadores ni cambiar la clave de guardado.
- No copiar juegos existentes (nombres, personajes o arte de otros juegos); las ideas de los fans se adaptan con arte y nombres propios.
