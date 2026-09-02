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

- **8 programas** de síntesis por osciladores: Grand Piano, Electric Piano (con trémolo),
  Draw Organ, Warm Strings, Analog Pad, Synth Lead, Synth Bass y Glass Bells.
- **Filtro** (cutoff + resonancia), **reverb**, envolvente (attack/release) y volumen, todo en vivo.
- **Polifonía real de 16 voces** con voice stealing, teclado visual que se ilumina y compresor a la salida.
- **Grabador con loop**: apretás REC, tocás, volvés a apretar y queda loopeando.
- **Metrónomo** de 50 a 200 BPM, agendado sobre el reloj del `AudioContext` (no derrapa).
- **Multitouch**: en celular podés hacer acordes con varios dedos.
- **Entra siempre en pantalla**: el teclado queda fijo abajo y los controles scrollean solos.
  La cantidad de octavas a la vista se adapta al ancho (3 en desktop, 2 en tablet, 1 en celular)
  para que la tecla nunca quede más angosta que un dedo.
- El **preset se guarda solo** en `localStorage` — programa, sliders, octava y BPM vuelven como los dejaste.

## 🎵 Cancionero

Ocho temas que se tocan solos iluminando las teclas para aprenderlas:

| Tema | Artista |
|------|---------|
| La Resaka | Supermerk2 |
| Se Te Ve la Tanga | Damas Gratis |
| No Me Arrepiento de Este Amor | Gilda |
| El Bombón Asesino | Los Palmeras |
| Mentirosa | Ráfaga |
| Soy Cordobés | Rodrigo |
| Fernet | Rei & Quevedo |
| Un Beso y una Flor | Nino Bravo |

Son transcripciones de oído del riff o el arpegio principal, no la partitura completa.
Viven en el objeto `SONGS` como pares `[nota MIDI, milisegundos]`, así que agregar o
corregir un tema es editar un array.

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
