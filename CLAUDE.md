# Portfolio de Victoria Molina de Castro (victoriamdc.com)

Este archivo es para Claude. Leelo completo antes de tocar cualquier cosa.

## Con quién trabajás

Vicu (Victoria) es **Product Designer, no desarrolladora**. Eso cambia cómo trabajás:

- Explicá en lenguaje simple, en español, sin jerga. Si usás un término técnico, aclaralo en media frase.
- Hacé vos el trabajo técnico (editar HTML/CSS, preparar imágenes, comandos). Ella decide contenido y diseño.
- Cuando ella tenga que hacer algo en la compu, dale **un paso por vez**, con el texto exacto a copiar y qué debería ver si salió bien.
- Antes de cambios grandes, mostrale qué vas a hacer y esperá su OK.
- **Nunca publiques** (git push, commit a main) sin que ella lo confirme explícitamente.
- Si pide algo que rompe las reglas de abajo, avisale y proponé una alternativa.

## Qué es el sitio

- Sitio estático: HTML + CSS + un poco de JS. Sin frameworks, sin build, sin npm.
- Repo: `github.com/victoriamolinadecastro/Portfolio`, rama `main`.
- El sitio está en la subcarpeta `Vectoria portfolio/` (ese es el nombre real, con "Vectoria").
- Vercel (proyecto `portfolio`) publica solo cada push a `main`. victoriamdc.com redirige a www.
- Idioma del sitio: inglés. Idioma con Vicu: español.

## Estructura

```
Vectoria portfolio/
├── index.html                 Home (card grande .featured + 2 .mini en .gallery)
├── work/index.html            Grilla de casos (a.work-card)
├── about/  contact/
├── onboarding-platform/       CASO DE REFERENCIA — copiar este para casos nuevos
├── kibit-media-kit/  kibitanalytics/  kibitreboot/  kibit/
├── aventura/  kibitwatch/  loserbaby/
├── assets/                    Todas las imágenes, .webp, con prefijo por caso
├── fonts/Defante.ttf
├── Victoria-Molina-de-Castro-CV.pdf
└── image-slot.js              <image-slot src="..."> en el sitio solo muestra la imagen
```

- Cada página es una carpeta con su `index.html` (URLs limpias).
- **El CSS está inline en cada página** (`<style>` en el `<head>`). No hay hoja compartida. Un cambio global se repite en todas.
- Links internos absolutos (`/work/`); assets relativos (`../assets/...`).
- Prefijos de assets: op (onboarding), mk (media kit), ka (analytics), kr (reboot), kibit, av (aventura), lb (loserbaby). Portadas viejas: `work-N.webp`.

## Reglas visuales (definidas por Vicu, no negociables)

1. Imágenes **sin border-radius propio**; las recorta su contenedor (`.ph`, `.wc-media`) con overflow hidden.
2. Cards **planas**: fondo `--surface` (#F2F2F2), **sin borde, sin sombra**. También cajas de diagramas y pasos.
3. Pills de cards en Work/Home: **máximo 2 términos** (`Experimentation / CRO`).
4. **Cada caso con portada distinta** (dispositivo, composición, fondo).
5. **Mucho aire** alrededor de mockups en portadas (se recortan distinto en Work, hero y Home).
6. Sombras solo en mockups de portadas y muy suaves.
7. **Más gráfico, menos texto.** Captura, flujo o número antes que párrafo.
8. Usar los componentes existentes; no inventar CSS si ya hay una clase.

Variables: `--bg #FFF`, `--text #333`, `--text-2 #808080`, `--surface #F2F2F2`, `--accent #FF0534`, `--footer #333`, títulos Defante (fallback Fredoka), texto Lato, `--page-max 1100px`.

Tamaños: card de Work 1600×1600 (`xx-card.webp`); hero y og:image 2880×1200 (`xx-hero-wide.webp`); destacado de Home 2400×1350 (`xx-featured.webp`); capturas internas 2400 px de ancho. Siempre .webp, idealmente < 200 KB.

Confidencialidad: difuminar o borrar nombres de clientes, logos y números reales que no tengan permiso.

## Copy

- Público: recruiters de Product / Growth / CRO / Data Designer. Escanean rápido.
- Inglés, frases cortas, verbos concretos. Título de sección = la idea ("Every change needed a developer"), no el tema.
- Cards de 1–2 líneas; máximo un párrafo por bloque.
- Mostrar método de growth: hipótesis, métrica principal, guardrails, resultado, aprendizaje. Números cuando se pueda.
- Mencionar trabajo AI-first cuando aplique.
- Frases ancla: hero "Product Designer for growth, experiments & data" / "I work AI-first, to go from idea to test in days."; footer "Design that feels right — and data that proves it."; Work "From Challenge to Solution".
- Fechas `MM.AA` (`06.26 → present`).

## Estructura de un caso (copiar onboarding-platform/index.html)

Nav (Work activo) → hero `.case-hero` (portada ancha, Back to Work, 3–4 `.tag`, h1, `.lead`, `.meta-tags` rol/equipo/fechas) → `.stat-row` (4 números) → 01 Context → 02 The problem (3 `.role-card`) → 03 My role (herramientas + cards) → 04+ solución (una sección por pieza, captura grande) → resultados `.dark-band` → `.outcome-card` What I learned (3 `.goal` con ícono Tabler) → `.next-case` → footer.

Componentes: `.ph.shot` (captura con zoom), `.split` / `.split-60` (imagen + card), `.solution-duo` (2 imágenes), `.duo` + `.info-card`, `.role-grid` + `.role-card`, `ol.flow.flow-col|flow-row` + `li.flow-step` (`.is-hot` resalta), `ul.quad-list`, `.ba-table`, `p.caption`, clase `reveal` para animación. Eyebrow numerado `<p class="eyebrow">04 — Título</p>` + `h2.sec-title`.

Head: `<title>Caso — Victoria Molina de Castro</title>`, meta description, `og:image` = hero ancho.

## Agregar un caso nuevo (checklist para vos)

1. Proponerle a Vicu historia, secciones y portada antes de construir.
2. Carpeta en minúsculas con guiones + prefijo de 2 letras único.
3. Imágenes en `assets/` (card, hero-wide, capturas), anonimizadas.
4. Duplicar `onboarding-platform/`, reemplazar todo, borrar secciones que sobren.
5. Card en `work/index.html` (copiar un `a.work-card`): href, aria-label, pill, wc-title, wc-desc, `image-slot` con id único y src.
6. Encadenar `.next-case`: el anterior apunta al nuevo, el nuevo al siguiente. (Hoy: Media Kit → Onboarding → Making Data Legible; casos viejos sin link.)
7. Home solo si se destaca: reemplazar `.featured` o un `.mini`. Criterio: casos de temas distintos.
8. QA: servir con `python3 -m http.server 8000` desde `Vectoria portfolio/` y revisar en `localhost:8000` (escritorio y mobile): imágenes, links, nav + CV, next case, pills, sin radios/bordes/sombras, sin datos confidenciales, title/og.
9. Publicar solo con OK de Vicu (ver abajo).

## Publicar

Vicu puede publicar de dos formas, las dos válidas; preguntale cuál prefiere y guiala paso a paso en esa:

- **Opción A, GitHub Desktop** (con botones, sin tokens): Summary con qué cambió → "Commit to main" → "Push origin".
- **Opción B, Terminal** (copiar y pegar): `cd ~/Desktop/Portfolio`, luego `git add -A && git commit -m "..."`, luego `git push`. Dale cada comando en su propio bloque para copiar, de a uno.

En las dos: después Vercel → Deployments → el último en "Ready" → abrir victoriamdc.com con Cmd+Shift+R.

Detalles de la Terminal: Usuario `victoriamolinadecastro`; password = token clásico con scope `repo` (pegar una sola vez; no se ve). Error "Invalid username or token" = token mal pegado o vencido. Credencial vieja guardada: `printf "protocol=https\nhost=github.com\n\n" | git credential-osxkeychain erase`. Nunca pedirle a Vicu que te muestre o pegue el token en el chat.

## Pendientes conocidos

- Confirmar si se pueden mostrar los números reales en las capturas/portadas de Onboarding (89%, "216 de 244"); si no, difuminar op-analytics, op-hero-wide, op-featured, op-card.
- Opcional: Next case en los casos viejos.
