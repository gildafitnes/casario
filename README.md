# Casa Río

Sitio estático (HTML + CSS, sin JavaScript ni build) para publicar en GitHub Pages.
Bilingüe: inglés en la raíz, español en `/es/`.

## Publicar en GitHub Pages

1. Sube todo el contenido de esta carpeta a la raíz del repositorio.
2. **Settings → Pages → Source: Deploy from a branch → Branch: `main` / `/ (root)`**.
3. En un par de minutos: `https://<usuario>.github.io/<repo>/`.

## Estructura

```
index.html               portada (EN)
why-this-matters.html    con las 6 fuentes enlazadas
phases.html              las fases, con sus 5 enlaces internos
inside.html              qué pasará dentro
cannot-buy.html          qué pasa si no podemos comprar
association.html         1.2 crear la asociación
contributions.html       cómo se gestionan las aportaciones
donations.html           PENDIENTE — donaciones
newsletter.html          PENDIENTE — newsletter
accounts.html            PENDIENTE — cuentas públicas
es/                      las mismas diez páginas en español
assets/css/style.css     todos los estilos
assets/fonts/            Montserrat Light + Light Italic (autoalojadas)
```

Los nombres de archivo son idénticos en los dos idiomas, así que el conmutador
ESP/ENG siempre lleva a la misma página en el otro idioma. Si añades una página
nueva, créala en los dos sitios con el mismo nombre y el conmutador funciona solo.

## Idioma

- Páginas en inglés: enlace **ESP** bajo el logo → `es/<misma-página>`
- Páginas en español: enlace **ENG** bajo el logo → `../<misma-página>`

## Mapa de enlaces

Portada:

| Elemento | Va a |
|---|---|
| `why this matters?` / `¿por qué importa esto?` | `why-this-matters.html` |
| `the first phase` / `la primera fase` | `phases.html` |
| `raising funds` / `captando fondos` (con elipse) | `donations.html` |
| `Where does your donation go?` / `¿A dónde va tu donación?` | `phases.html` |
| `What will happen inside?` / `¿Qué pasará dentro?` | `inside.html` |
| `Donate to Casa Río` / `Donar a Casa Río` (con elipse) | `donations.html` |

Fases: contribuciones, asociación, newsletter, cuentas y "y si no podemos comprar".
El logo enlaza siempre a la portada del idioma en el que estás.

## Animaciones

Todo con CSS y SVG, sin JavaScript.

- **Punto orbital**: un círculo recorre la elipse con `<animateMotion>` siguiendo
  el trazado real (`<mpath>`), así que va exactamente por encima de la línea.
  Está en el logo (24 s), en *raising funds* (18 s) y en *Donate* (26 s).
- **Blobs**: escala de 1 a 1.06 en ciclos de 10–14 s, con retardos distintos para
  que no vayan sincronizados.

Con `prefers-reduced-motion` activado, el punto se queda quieto abajo del todo
(`.orbit-dot-still`) y los blobs dejan de latir.

## Retocar cosas

Variables al principio de `assets/css/style.css`:

```css
--green:   #006600;
--yellow:  #ffd600;   --magenta: #ff70ff;
--cyan:    #00ffff;   --lime:    #a5ff5f;
--measure: 44rem;                        /* ancho de la columna de texto */
--gap-block: clamp(6rem, 15vw, 11rem);   /* separación entre bloques */
```

**Tamaño del punto.** El del logo es `r="4.7"` dentro de un `viewBox` de 300
unidades: equivale a los 14 px de Photoshop sobre un lienzo de 1080. Los de
*raising funds* y *Donate* son `r="12"` porque su `viewBox` mide 100 unidades de
alto en vez de 106. Si cambias uno, cambia los tres para que se vean iguales.

**Elipses de texto.** Cada una lleva un `viewBox` cuya proporción coincide con la
caja del texto que rodea, para que el punto salga redondo y no ovalado. Si cambias
el texto de dentro, hay que recalcular el ancho del `viewBox`:
`ancho = (avance_del_texto_en_em + 0.36) * 1.06 / 1.593 * 100`, redondeado.
El alto siempre es 100 y `rx` es la mitad del ancho.

**Latido de los blobs.** Solo hay que tocar el `scale(1.06)` del `@keyframes pulse`.

## Tipografía

Montserrat Light y Light Italic van autoalojadas en `assets/fonts/`. No se carga
nada de Google Fonts, así que el logo sale en cursiva real siempre, también sin
conexión.
