# Blueprint — Diseño de Interfaz
## Design System + Pantallas de AyudaYa (prototipo de alta fidelidad codificado)

> **Cómo usar este documento:** Este es el *spec* que vas a entregar a tu agente de IA (Kilocode). Pégalo completo como primer mensaje. NO lo resumas ni lo cortes — la comparación entre modelos solo es válida si todos los grupos parten del mismo spec exacto. Cuando termines con la IA-A, repite el proceso con la IA-B usando este mismo documento, partiendo de cero.

---

## 1. Contexto del problema

AyudaYa es una plataforma para que ciudadanos de sectores urbano-marginales de Guayaquil reporten necesidades comunitarias (baches, alumbrado, inseguridad) y líderes comunitarios las gestionen. El usuario final **no es técnico**: la interfaz tiene que ser obvia, legible y usable bajo condiciones reales (pantallas pequeñas, posible baja alfabetización digital, uso a una mano en la calle).

Tu trabajo en esta materia es el **sistema visual y las pantallas**, no la lógica de negocio. Construyes un prototipo de alta fidelidad *codificado* en HTML y CSS puro.

---

## 2. Stack y restricciones

- **HTML5 + CSS3 puro.** Sin frameworks de CSS (sin Bootstrap, sin Tailwind), sin preprocesadores (sin Sass).
- **JavaScript:** solo el mínimo para interacciones visuales (abrir/cerrar un menú, cambiar de pantalla). No hay datos reales ni backend.
- **Design tokens obligatorios:** todo color, tamaño de fuente, espaciado, radio y sombra se define como **CSS custom properties** (`--color-primary`, `--space-md`, etc.) en `:root`. Ningún valor "mágico" hardcodeado dentro de los componentes.
- **Responsive:** mobile-first. Las pantallas deben verse bien a 360px de ancho (móvil) y adaptarse a escritorio.
- **Accesibilidad mínima:** contraste suficiente (texto legible sobre fondo), tamaños de toque adecuados (mínimo 44px de alto en botones), HTML semántico (`<button>`, `<nav>`, `<main>`, `<label>` asociado a su input).
- **Sin librerías externas de iconos por CDN.** Usa SVG inline o caracteres unicode simples si necesitas iconos.

---

## 3. Entregables

Estructura de archivos esperada:

```
ayudaya-design/
├── index.html          (style guide viva — muestra TODO el sistema)
├── login.html
├── reportes.html       (listado de reportes)
├── crear-reporte.html
└── css/
    └── styles.css      (tokens + componentes, un solo archivo)
```

### 3.1 Design tokens (`:root` en styles.css)
- **Paleta:** color primario, secundario, de éxito, de alerta/error, neutrales (al menos 3 grises), fondo, superficie. Justifica la elección cromática implícitamente: debe transmitir confianza institucional + cercanía comunitaria.
- **Tipografía:** familia(s), y una escala de al menos 4 tamaños (título, subtítulo, cuerpo, caption).
- **Espaciado:** escala de al menos 4 pasos (ej. 4, 8, 16, 24px).
- **Radios y sombras:** al menos 2 radios y 2 niveles de elevación.

### 3.2 Componentes core (5)
Cada uno debe existir, estar estilizado con los tokens, y mostrarse en la style guide:
1. **Botón** — en sus variantes: primario, secundario, y estado deshabilitado.
2. **Input de texto** — con `<label>`, estado normal y estado de error (con mensaje).
3. **Card de reporte** — muestra: título del reporte, categoría, estado, fecha y una línea de ubicación. Es el componente más importante; se reutiliza en el listado.
4. **Badge** — para estado (ej. *Pendiente*, *En proceso*, *Resuelto*) y para categoría (ej. *Bache*, *Alumbrado*, *Inseguridad*). Cada valor con su color semántico.
5. **Navbar / barra de navegación** — apropiada para móvil (puede ser barra inferior o superior).

### 3.3 Pantallas (3)
1. **Login** (`login.html`): logo/nombre AyudaYa, campos usuario y contraseña (usa el componente input), botón primario "Ingresar", enlace secundario "Crear cuenta". Centrado, limpio.
2. **Listado de reportes** (`reportes.html`): navbar + un listado de al menos 4 cards de reporte con datos de ejemplo variados (distintas categorías y estados) + un botón flotante o destacado "Nuevo reporte".
3. **Crear reporte** (`crear-reporte.html`): formulario con campos para título, categoría (selector), descripción, un placeholder visual para "foto" y otro para "ubicación en mapa" (NO tiene que funcionar, es un recuadro con su label), y botón primario "Enviar reporte".

### 3.4 Style guide viva (`index.html`)
Una sola página que documenta el sistema: muestra la paleta con sus nombres de token, la escala tipográfica, los espaciados, y **todos los componentes** en sus variantes. Es la "fuente de verdad" del design system. Enlaza a las 3 pantallas.

---

## 4. Criterios de aceptación (checklist verificable)

El prototipo está **completo** solo si:

- [ ] Existen los 5 archivos HTML + el styles.css con la estructura indicada.
- [ ] `:root` contiene tokens para paleta, tipografía, espaciado, radios y sombras. Ningún color o tamaño hardcodeado en los componentes (todo vía `var(--...)`).
- [ ] Los 5 componentes existen y se ven correctamente en `index.html`.
- [ ] El botón tiene sus 3 variantes (primario, secundario, deshabilitado) visualmente distintas.
- [ ] El input muestra estado de error con mensaje.
- [ ] La card de reporte se reutiliza en `reportes.html` con datos distintos.
- [ ] Los badges de estado y categoría tienen colores semánticos diferenciados.
- [ ] Las 3 pantallas existen y son navegables (los enlaces funcionan).
- [ ] Todo se ve correctamente a 360px de ancho sin scroll horizontal ni elementos cortados.
- [ ] Los botones tienen mínimo 44px de alto; los inputs tienen `<label>` asociado.
- [ ] El contraste de texto es legible (no gris claro sobre blanco).

---

## 5. Definition of Done

1. Abres `index.html` en el navegador y ves el sistema completo sin errores de consola.
2. Navegas a las 3 pantallas y de vuelta; todos los enlaces funcionan.
3. Reduces la ventana a ancho de móvil (~360px): nada se rompe, nada requiere scroll horizontal.
4. Revisas el CSS: confirmas que los componentes usan `var(--token)` y no valores sueltos.
5. Un compañero que no construyó esto entiende cada pantalla sin que se la expliques.

---

## 6. Qué NO hacer

- No usar Bootstrap, Tailwind, Material, ni ninguna librería de CSS.
- No conectar a ninguna API ni base de datos.
- No inventar funcionalidad de research de usuarios ni "resultados de tests de usabilidad" — eso no es parte de este entregable.
- No hardcodear colores/tamaños dentro de los componentes saltándote los tokens.
