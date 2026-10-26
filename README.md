# 🎹 Teclado Villero — Piano Villero X50

Sintetizador web al estilo **Korg X50**, hecho con **Web Audio API**. Se toca con el
teclado de la compu (QWERTY), el mouse o la pantalla táctil. Todo en un solo archivo
`index.html`, sin dependencias ni instalación.

Un proyecto de [fizz.software](https://fizz.software).

## ▶️ Cómo usarlo

Cloná la repo y levantá un servidor local:

```bash
git clone git@github.com:skyze2002/Teclado-Villero.git
cd Teclado-Villero
python3 -m http.server 8123
```

Después abrí **http://localhost:8123/** en el navegador.

> También podés abrir `index.html` directo, pero es más confiable por `localhost`.

## 🎛️ Qué tiene

- **9 programas** de síntesis por osciladores: Piano Acústico (el de fábrica, síntesis aditiva
  con armónicos), Grand Piano, Electric Piano (con trémolo), Draw Organ, Warm Strings, Analog Pad,
  Synth Lead, Synth Bass y Glass Bells.
- **Filtro** (cutoff + resonancia), **reverb**, envolvente (attack/release) y volumen, todo en vivo.
- **Polifonía real de 16 voces** con voice stealing, teclado visual que se ilumina y compresor a la salida.
- **Grabador con loop**: apretás REC, tocás, volvés a apretar y queda loopeando.
- **Metrónomo** de 50 a 200 BPM, agendado sobre el reloj del `AudioContext` (no derrapa).
- **Multitouch**: en celular podés hacer acordes con varios dedos.
- **Entra siempre en pantalla**: el teclado queda fijo abajo y los controles scrollean solos.
  La cantidad de octavas a la vista se adapta al ancho (3 en desktop, 2 en tablet, 1 en celular)
  para que la tecla nunca quede más angosta que un dedo.
- El **preset se guarda solo** en `localStorage` — programa, sliders, octava, BPM y velocidad
  del cancionero vuelven como los dejaste.

## 🎵 Cancionero

Nueve temas que se tocan solos iluminando las teclas. Cada uno es la **base de acompañamiento**
del tema: tonalidad, progresión de acordes y tempo sacados de cifrados públicos, tocados con el
ritmo típico del género (tresillo villero, bajo + acorde a contratiempo de la cumbia y el
cuarteto, arpegio de balada). No incluye la melodía: la base suena como el tema y la melodía la
tocás vos encima.

Al elegir un tema **se configura solo**: carga el timbre y los ajustes (filtro, reverb, envolvente)
que mejor le quedan, y arranca con su **ritmo de batería**. Después podés retocar todo a mano.

| Tema | Artista | Tono | Tempo | Base | Timbre | Ritmo |
|------|---------|------|-------|------|--------|-------|
| La Resaka | Supermerk2 | La menor | ≈100 | tresillo villero | Synth Lead | villero |
| Se Te Ve la Tanga | Damas Gratis | Re menor | ≈98 | tresillo villero | Synth Lead | villero |
| No Me Arrepiento de Este Amor | Gilda | Do menor | ≈150 | contratiempo | Draw Organ | cumbia |
| El Bombón Asesino | Los Palmeras | Re menor | ≈100 | contratiempo | Draw Organ | cumbia |
| Mentirosa | Ráfaga | Fa menor | ≈94 | contratiempo | Synth Lead | cumbia |
| Soy Cordobés | Rodrigo | Mi menor | ≈125 | tunga-tunga | Piano Acústico | cuarteto |
| Fernet | Rei & Quevedo | Fa# menor | ≈100 | arpegio | Electric Piano | pop |
| Un Beso y una Flor | Nino Bravo | La mayor | 83 | arpegio de balada | Piano Acústico | balada |
| No Somos Perfectos | Lauta, Valentino Merlo & Tote | a confirmar | 87 | — | Piano Acústico | cumbia |

`≈` = tempo estimado (no hay dato publicado). El slider **Velocidad** (50–150%) lo ajusta en
vivo, así lo emparejás de oído con la grabación.

*No Somos Perfectos* salió en agosto de 2026 y todavía no hay acordes publicados: por ahora toca
sólo el ritmo a su tempo real. Cuando se confirme la progresión, se carga en su `seq`.

### 🥁 Ritmo

Batería sintetizada en vivo (bombo, redoblante, rim, hi-hat, timbal, congas y güiro, todo con
osciladores y ruido, sin samples), con un patrón por género: `villero`, `cumbia`, `cuarteto`,
`balada` y `pop`. Se prende/apaga con **RITMO** y tiene su propio volumen.

Notas y batería se agendan juntas sobre el reloj del `AudioContext` (con lookahead, como el
metrónomo), así van siempre a tiempo aunque cambies la velocidad en el medio.

### Agregar un tema

Los temas viven en el objeto `SONGS`: cada evento es `[nota, beats]`, donde la nota es un MIDI,
un array de MIDIs (acorde) o `null` (silencio), y los helpers `trip`, `contra`, `arp` y `ballad`
arman un compás por acorde. Cada tema lleva además `sound` (timbre y ajustes) y `groove` (ritmo).
Agregar uno es escribir su progresión, tono, tempo, sonido y ritmo.

## ⌨️ Cómo tocar

| Zona | Teclas |
|------|--------|
| Notas graves | `Z S X D C V G B H N J M` |
| Notas agudas | `Q 2 W 3 E R 5 T 6 Y 7 U` |
| Cambiar octava | flechas `←` / `→` |

También se puede tocar con el mouse arrastrando sobre las teclas, o con el dedo en el celular.

## 🚀 Deploy

Es un sitio estático de un solo archivo: alcanza con servirlo. Con nginx en un VPS:

```nginx
server {
    listen 80;
    server_name teclado.tudominio.com;
    root /var/www/teclado-villero;
    index index.html;
}
```

Después `sudo certbot --nginx -d teclado.tudominio.com` para el HTTPS. También anda
tal cual en GitHub Pages, Netlify, Vercel o Cloudflare Pages.

> Antes de publicar, en el `<head>` hay dos meta tags `og:url` y `og:image` comentadas:
> descomentalas con la URL absoluta de tu dominio para que el link se vea bien al compartirlo.

## 🛠️ Tecnología

HTML + CSS + JavaScript puro con **Web Audio API**. Sin frameworks, sin build, sin dependencias.
El logo va embebido en base64, así que el `index.html` se sigue bancando solo.
