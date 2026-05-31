# DIU - Practica 4, entregables

## Equipo: DIU3_DarkPatterns
**Proyecto:** ClearBurger — Aplicación web de restaurante sin dark patterns

**App publicada:** [clearburger-diu3.surge.sh](https://clearburger-diu3.surge.sh)

---

## Entorno de producción

Stack tecnológico utilizado:

| Herramienta | Versión | Rol |
|---|---|---|
| React | 19 | Framework UI |
| Vite | 8 | Bundler / dev server |
| Tailwind CSS | v4 | Motor de estilos utility-first |
| shadcn/ui | Nova preset | Componentes Radix accesibles |
| Lucide React | — | Iconografía |
| React Router DOM | v7 | Enrutado cliente |
| Storybook | v10 | Documentación de componentes |

---

## Arquitectura de componentes (Atomic Design)

```
src/
├── components/
│   ├── atoms/
│   │   ├── Button.jsx        # 4 variantes: primary, secondary, ghost, disabled
│   │   ├── Tag.jsx           # 3 variantes: default (verde), warning (ámbar), neutral (gris)
│   │   └── Input.jsx         # 3 estados: default, focus (#D92525), error (#EF4444)
│   ├── molecules/
│   │   ├── SearchBar.jsx     # Buscador con icono Lucide, estado controlado
│   │   └── IngredientButton.jsx  # Botón toggle para selección de ingredientes
│   └── organisms/
│       ├── Navbar.jsx        # Barra flotante fija (píldora), logo + navegación
│       ├── Footer.jsx        # Footer estructurado con grid de enlaces y RRSS
│       └── FooterSVGs.jsx    # Iconos SVG: Instagram, Twitter/X, TikTok, LinkedIn
├── pages/
│   ├── Home.jsx              # Hero + 3 destacadas + sección "Por qué ClearBurger"
│   ├── Carta.jsx             # 9 productos, filtro por categoría + búsqueda
│   ├── Customizar.jsx        # Personalizador con 5 categorías y resumen sticky
│   └── Reservar.jsx          # Formulario con validación inline y confirmación
├── stories/                  # Stories de Storybook por componente
└── index.css                 # Tokens del Design System (colores, fuentes, dark mode)
```

---

## Páginas implementadas

### Home
Hero con imagen de fondo (overlay oscuro), titular y CTA principal. Grid de 3 hamburguesas destacadas con foto, tags y precio. Sección informativa "Por qué ClearBurger" con los tres valores del proyecto (transparencia, calidad, sin dark patterns).

### Carta
Grid de 9 hamburguesas con buscador en tiempo real y filtros por categoría (Todas / Clásicas / Premium / Gourmet / Vegetarianas). Cada tarjeta muestra imagen, tags de alérgenos/características, descripción, precio y botón de pedido. Estado vacío con mensaje informativo si no hay resultados.

### Customizar
Personalizador dividido en dos columnas: panel de ingredientes (5 categorías: Base, Quesos, Vegetales, Extras, Salsas) con botones toggle, y panel de resumen sticky con desglose de precios, total en tiempo real y botón de añadir al pedido (desactivado hasta seleccionar base).

### Reservar
Formulario de reserva con validación inline (nombre, email, teléfono, personas, fecha, hora). Los campos muestran estado de error en rojo con mensaje descriptivo. Sin depósito ni registro obligatorio. Pantalla de confirmación con resumen de la reserva.

---

## Documentación con Storybook

Stories documentadas con `autodocs`:

| Componente | Categoría | Stories |
|---|---|---|
| Button | Atoms | Primary · Secondary · Ghost · Disabled |
| Tag | Atoms | Default · Warning · Neutral |
| Input | Atoms | Default · Focus · Error |
| SearchBar | Molecules | Default · Activo · Error |
| IngredientButton | Molecules | Disponible · Seleccionado · Agotado |

Lanzar Storybook: `npm run storybook` (puerto 6006)

---

## Tokens de diseño (Design System)

| Token | Valor | Uso |
|---|---|---|
| `#1A1A1A` | Background | Fondo de app y secciones |
| `#222222` | Surface | Cards, formularios, paneles |
| `#2B2B2B` | Surface alt | Navbar, Footer |
| `#333333` | Border | Bordes, estado inactivo |
| `#D92525` | Primary | CTA principal, acento |
| `#B71D1D` | Primary dark | Hover de CTA |
| `#D97E00` | Accent | Botón "Crea tu hamburguesa" |
| `#F5F5F5` | Text | Texto principal |
| `#8C8C8C` | Muted | Texto secundario |
| Montserrat 700 | Font heading | Títulos |
| Inter 400/500 | Font body | Cuerpo y UI |

---

## Briefing

El punto de partida para la implementación fue el Design System desarrollado en la P3 en Figma. Se tradujo directamente a código la misma jerarquía de componentes (Atomic Design), los mismos tokens de color y tipografía, y la misma estructura de páginas del prototipo Hi-Fi. Tailwind CSS v4 gestionó los estilos con clases utilitarias directamente en los componentes, eliminando la necesidad de ficheros CSS separados por componente y manteniendo todo el sistema de tokens en `index.css`.

Para la implementación de los componentes interactivos se priorizó la fidelidad funcional al prototipo: la Carta filtra en tiempo real por categoría y texto simultáneamente, el Customizar calcula el precio acumulado conforme se seleccionan ingredientes, y el Reservar valida cada campo individualmente con mensajes de error específicos. Estos comportamientos responden directamente a los flujos que se definieron en el User Journey de la P1 y se materializaron en el wireframe de la P2.

Storybook permitió documentar los componentes del Design System de forma viva: cada story refleja un estado visual real del componente tal como aparece en la aplicación, con fondos en dark mode y los mismos estilos del sistema de diseño. Esto crea un nexo directo entre la documentación y la implementación, facilitando la consistencia y la evaluación de accesibilidad de cada elemento de forma aislada.
