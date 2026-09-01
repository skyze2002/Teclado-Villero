# 🎹 Teclado Villero — Piano Villero X50

Sintetizador web al estilo **Korg X50**, hecho con **Web Audio API**. Se toca con el
teclado de la compu (QWERTY), el mouse o la pantalla táctil. Todo en un solo archivo
`index.html`, sin dependencias ni instalación.

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
- Polifonía de 16 voces, teclado visual que se ilumina y compresor a la salida.
- **Canciones que se tocan solas** iluminando las teclas para aprenderlas:
  - 🍺 **La Resaka** — Supermerk2 (riff del intro)
  - 🥃 **Fernet** — Rei & Quevedo (arpegio de acordes)
  - 🌹 **Un Beso y una Flor** — Nino Bravo (intro con bajo descendente)

## ⌨️ Cómo tocar

| Zona | Teclas |
|------|--------|
| Notas graves | `Z S X D C V G B H N J M` |
| Notas agudas | `Q 2 W 3 E R 5 T 6 Y 7 U` |
| Cambiar octava | flechas `←` / `→` |

También se puede tocar con el mouse arrastrando sobre las teclas.

## 🛠️ Tecnología

HTML + CSS + JavaScript puro con **Web Audio API**. Sin frameworks, sin build, sin dependencias.
