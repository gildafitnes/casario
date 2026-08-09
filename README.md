# Casa Río

Sitio estático (HTML + CSS, sin dependencias ni build) para publicar en GitHub Pages.

## Publicar en GitHub Pages

1. Crea un repositorio nuevo y sube todo el contenido de esta carpeta a la raíz.
2. En el repo: **Settings → Pages → Source: Deploy from a branch → Branch: `main` / `/ (root)`**.
3. En un par de minutos estará en `https://<usuario>.github.io/<repo>/`.

No hace falta nada más: `index.html` está en la raíz y todas las rutas son relativas.

## Estructura

```
index.html              portada
why-this-matters.html   con las 6 fuentes como enlaces reales
phases.html             las fases, con sus 5 enlaces internos
inside.html             qué pasará dentro
cannot-buy.html         qué pasa si no podemos comprar
association.html        1.2 crear la asociación
contributions.html      cómo se gestionan las contribuciones
donations.html          PENDIENTE — página de donaciones
newsletter.html         PENDIENTE — alta en la newsletter
accounts.html           PENDIENTE — cuentas públicas en vivo
assets/css/style.css    todos los estilos
assets/fonts/           Montserrat-Light.ttf (respaldo si Google Fonts falla)
```

## Mapa de enlaces

Portada:

| Elemento | Va a |
|---|---|
| `why this matters?` | `why-this-matters.html` |
| `the first phase` | `phases.html` |
| `raising funds` (con círculo) | `donations.html` |
| `Where does your donation go?` | `phases.html` |
| `What will happen inside?` | `inside.html` |
| `Donate to Casa Río` | `donations.html` |

Fases:

| Elemento | Va a |
|---|---|
| `[How are contributions managed? →]` | `contributions.html` |
| `[Legal structure and costs →]` | `association.html` |
| `[subscribe to the newsletter →]` | `newsletter.html` |
| `[Follow the acquisition fund →]` | `accounts.html` |
| `[What happens if we cannot buy? →]` | `cannot-buy.html` |

El logo enlaza siempre a la portada.

## Animaciones

Todo con CSS, sin JavaScript.

- **Logo**: dos elipses SVG superpuestas que respiran a ritmos distintos (9 s y 13 s), con rotación y proporción ligeramente cambiantes. Se acelera al pasar el cursor.
- **Blobs**: escala de 1 a 1.06 en ciclos de 10–14 s, cada uno con retardo distinto para que no vayan sincronizados.
- **`raising funds`**: su elipse usa la misma animación que el logo, a 6.5 s.

Se respeta `prefers-reduced-motion`: si el sistema del visitante pide movimiento reducido, todo queda quieto.

## Retocar cosas

Casi todo está en las variables del principio de `assets/css/style.css`:

```css
--green:   #006600;   /* el verde de todo el texto */
--yellow:  #ffd600;   /* blob 1 */
--magenta: #ff70ff;   /* blob 2 */
--cyan:    #00ffff;   /* blob 3 */
--lime:    #a5ff5f;   /* blob 4 */
--measure: 44rem;     /* ancho máximo de la columna de texto */
--gap-block: clamp(6rem, 15vw, 11rem);  /* separación entre bloques de la portada */
```

Cada blob tiene su propia regla (`.blob--yellow`, `.blob--magenta`, …) donde se ajusta
posición (`left` / `top`), tamaño (`width`) y desenfoque (`filter: blur()`).

Para cambiar la intensidad del latido, edita el `@keyframes pulse`: el `scale(1.06)`
es lo único que hay que tocar.

## Tipografía

Montserrat Light se carga desde Google Fonts (incluye la cursiva real). El archivo
`Montserrat-Light.ttf` queda autoalojado como respaldo por si Google no está disponible.
