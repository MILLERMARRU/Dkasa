# Dikassa — Landing Page

Landing page oficial de **Constructora e Ingeniería Dikassa S.A.C.**, empresa peruana especializada en el programa habitacional **Techo Propio** en Nueva Cajamarca, San Martín.

Construí el sitio como una experiencia visual de una sola página que guía al visitante desde el exterior hasta el interior de una vivienda real mediante una animación de **288 frames WebP** controlada por scroll, antes de presentar la empresa, sus servicios y sus datos de contacto.

---

## Vista general

```
Animación scroll-driven (288 frames) → Nosotros → Servicios → Techo Propio → Proyectos → Contacto
```

- **Sin frameworks JS** — Astro puro, sin React ni Vue
- **Sin base de datos** — sitio completamente estático
- **GSAP ScrollTrigger** controla el canvas frame a frame
- **Paleta extraída de los renders** — madera cálida, hueso y carbón

---

## Stack

| Tecnología | Versión | Uso |
|---|---|---|
| [Astro](https://astro.build) | 6.x | Generador de sitio estático |
| [GSAP](https://gsap.com) | 3.15 | Animación scroll del hero |
| Node.js | ≥ 22.12 | Entorno de desarrollo |

---

## Estructura del proyecto

```
├── public/
│   ├── frames/          → 288 frames WebP para la animación scroll (frame-0001 … frame-0288)
│   ├── images/          → Renders y fotos de proyectos (jpg)
│   ├── favicon.svg
│   └── favicon.ico
│
├── src/
│   ├── assets/          → SVGs procesados por Astro <Image />
│   ├── layouts/
│   │   └── Layout.astro → Shell HTML, variables CSS, tipografías, reveal global
│   ├── components/
│   │   ├── Navbar.astro       → Barra de navegación fija con CTA WhatsApp
│   │   ├── HeroScroll.astro   → Hero con 288 frames en canvas + GSAP
│   │   ├── Nosotros.astro     → Identidad y valores de Dikassa
│   │   ├── Servicios.astro    → Carta de servicios de la constructora
│   │   ├── TechoPropio.astro  → Explicación del programa habitacional
│   │   ├── Proyectos.astro    → Galería de renders de viviendas
│   │   ├── Contacto.astro     → Datos de contacto y WhatsApp
│   │   ├── Footer.astro       → Pie de página con links y datos legales
│   │   └── Welcome.astro      → Pantalla de bienvenida (reserva)
│   └── pages/
│       └── index.astro  → Página principal que ensambla todos los componentes
│
├── astro.config.mjs
├── tsconfig.json
└── package.json
```

---

## Comandos

Todos se ejecutan desde la raíz del proyecto:

| Comando | Acción |
|---|---|
| `npm install` | Instala las dependencias |
| `npm run dev` | Levanta el servidor de desarrollo en `localhost:4321` |
| `npm run build` | Genera el build estático en `./dist/` |
| `npm run preview` | Previsualiza el build antes de deployar |

---

## Animación hero — cómo funciona

Extraje 288 frames WebP del video del recorrido por la vivienda y los cargo de forma progresiva en un `<canvas>` retina-aware. GSAP ScrollTrigger mapea la posición de scroll al índice de frame, logrando el efecto de "tour en video" sin reproducir ningún archivo de video en el cliente.

```js
// Carga progresiva: primeros 40 frames inmediatos, resto en lotes de 30
await Promise.all(Array.from({ length: 40 }, (_, i) => loadFrame(i + 1)))
// …luego en batches de 30 con pausa de 16ms entre lotes
```

El canvas escala en modo **cover** para cubrir toda la ventana a cualquier resolución.

---

## Paleta de colores

| Variable CSS | Hex | Uso |
|---|---|---|
| `--color-bone` | `#F5F2EE` | Textos claros, fondo light |
| `--color-madera` | `#C8965A` | Acento principal |
| `--color-terracota` | `#D4621A` | Acento secundario |
| `--color-carbon` | `#141412` | Fondo oscuro, base |
| `--color-gris` | `#3A3A3A` | Textos, muebles |

---

## Tipografías

- **Cormorant Garamond** — títulos y display (peso 400/500, normal e itálica)
- **Geist** — cuerpo de texto y UI (peso 300/400/500/600)

Ambas se cargan desde Google Fonts con `preconnect` para minimizar el tiempo de bloqueo.

---

## Contacto del cliente

- **WhatsApp:** 917 516 901
- **Dirección:** Jr. Tacna c/ Jr. San Luis, Nueva Cajamarca, San Martín, Perú
- **Programa:** Techo Propio — Bono Familiar Habitacional (BFH)
