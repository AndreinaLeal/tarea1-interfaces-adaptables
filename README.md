# Tarea 1 — Construcción de interfaces web adaptables con HTML y CSS

## Identificación

- **Estudiante:** Andreina Leal
- **Curso:** Programación web avanzada (SOFT-12)
- **Sección:** SCV2
- **Docente:** Álvaro Cordero Peña
- **Fecha de entrega:** 20 de setiembre de 2026

## Descripción de los casos

### Caso 1 — Centro de control de una expedición científica

Interfaz tipo panel de control para una expedición científica en Costa Rica. Permite
visualizar de un vistazo el estado general de la operación: resumen de indicadores,
misiones activas con su estado, equipos científicos, alertas con distintos niveles de
importancia y una agenda de próximas actividades. El problema a resolver es de
organización visual: mostrar simultáneamente varias zonas de información sin perder
jerarquía ni claridad, priorizando la lectura rápida por parte del equipo coordinador.

### Caso 2 — Panel público de información de un festival

Interfaz pensada para que los asistentes de un festival cultural consulten desde su
teléfono qué está pasando en cada momento. El problema a resolver es mobile-first:
la sección "Ahora" debe ser lo primero y más visible en pantallas pequeñas, mientras
que en pantallas grandes se debe poder comparar la programación de varios escenarios
al mismo tiempo.

## Estructura de carpetas

```
Tarea1/
├── README.md
├── caso1/
│   ├── index.html
│   ├── css/
│   │   └── estilos.css
│   └── img/
└── caso2/
    ├── index.html
    ├── css/
    │   └── estilos.css
    └── img/
```

## Instrucciones para abrir cada caso

Cada caso es independiente y funciona por sí solo. Para verlo:

1. Cloná o descargá el repositorio.
2. Abrí `caso1/index.html` directamente en el navegador para ver el Caso 1.
3. Abrí `caso2/index.html` directamente en el navegador para ver el Caso 2.
4. Para probar la adaptabilidad, se recomienda usar las herramientas de desarrollador
   del navegador (F12 → modo de dispositivo) o simplemente redimensionar la ventana.

## Decisiones de diseño

**¿Por qué seleccionó determinadas etiquetas semánticas?**
Se usó `header` para agrupar la identidad de cada página (título y datos generales),
`nav` para la navegación principal, `main` para el contenido central único de la
página, `section` para agrupar bloques de contenido con su propio título (`h2`),
`article` para elementos que tienen sentido por sí mismos dentro de una lista (por
ejemplo cada indicador o cada escenario), `aside` para el bloque de alertas del Caso 1
por ser información complementaria al contenido principal, y `footer` para el cierre
de cada página. No se usaron etiquetas por su apariencia visual sino por el
significado del contenido que agrupan.

**¿Cómo organizó la jerarquía de encabezados?**
Cada página tiene un único `h1` (el título general), los `h2` marcan cada sección
principal (Resumen, Misiones, Equipos, Alertas, Agenda en el Caso 1; Ahora,
Programación, Cambios, Servicios en el Caso 2), y los `h3` se usan dentro de cada
tarjeta o elemento individual (por ejemplo el nombre de una misión o de un escenario).

**¿Cómo incorporó la accesibilidad básica?**
Se declaró `lang="es"` en el `html`. Los estados de las misiones y las alertas no
dependen únicamente del color: las misiones usan además el texto en `<strong>` con la
palabra del estado, y las alertas usan un símbolo de texto (`!!`, `!`, `i`) generado
con `::before` además de su color. Se usó `aria-label` en la navegación y
`aria-labelledby` en las secciones para vincularlas con su título. Se cuidó el
contraste entre texto y fondo en toda la paleta de colores.

**¿Cómo funciona el modelo de caja en sus principales componentes?**
Se aplicó `box-sizing: border-box` de forma global para que el padding y el border no
alteren el ancho definido de los elementos. Las tarjetas (misiones, equipos, alertas,
escenarios) usan `padding` interno para separar el contenido de su borde y `gap` en
sus contenedores en vez de márgenes individuales, evitando así valores arbitrarios.

**¿Dónde utilizó posicionamiento, cuál valor de position empleó y por qué?**
- Caso 1: el `header` usa `position: sticky` para que el nombre de la expedición y su
  estado general permanezcan visibles mientras se hace scroll por el panel.
- Caso 2: la `nav` usa `position: sticky` para que las opciones de navegación sigan
  accesibles mientras el usuario recorre el contenido desde su teléfono; además, la
  etiqueta "En este momento" usa `position: absolute` dentro de un contenedor con
  `position: relative` (`.actividad-ahora`) para superponerse sobre la tarjeta de cada
  actividad en curso.

**¿Por qué algunos estilos prevalecen sobre otros?**
Se trabajó con clases reutilizables (por ejemplo `.mision`, `.mision--en-progreso`) en
vez de IDs para los estilos visuales, aprovechando que una clase más específica
(`.mision--critica`) sobrescribe a la clase base (`.mision`) de forma natural por el
orden de la cascada, sin necesidad de `!important`.

**¿Dónde utilizó Flexbox y por qué?**
En ambos casos se usó Flexbox para: la navegación (alinear los enlaces en fila con
espacio entre ellos), los indicadores del resumen y las tarjetas de "Ahora" (distribuir
elementos de tamaño similar con `flex-wrap`), y el encabezado de cada misión/alerta
(alinear ícono y texto). Flexbox se eligió en todos los casos donde la distribución es
unidimensional (una fila o una columna).

**¿Dónde utilizó CSS Grid y por qué?**
El requisito principal de Grid en el Caso 1 se resuelve en el `main` a partir de
1024px con `grid-template-areas`, distribuyendo resumen, misiones, alertas, equipos y
agenda en varias zonas simultáneas. En el Caso 2, la sección de "Programación por
escenarios" usa Grid para mostrar los cuatro escenarios en columnas, y en escritorio
el `main` también usa `grid-template-areas` para reorganizar Ahora, Programación,
Cambios y Servicios. Grid se usó donde el problema era bidimensional (filas y
columnas a la vez), a diferencia de Flexbox.

**¿Cómo cambia el layout entre teléfono, tableta y escritorio?**
- Teléfono: una sola columna en ambos casos, priorizando lo más importante (estado
  general en el Caso 1, sección "Ahora" en el Caso 2).
- Tableta: se introducen 2 columnas en elementos como equipos científicos o los
  escenarios del festival, aprovechando el espacio extra sin saturar la pantalla.
- Escritorio: ambos casos reorganizan completamente el `main` con `grid-template-areas`
  para mostrar varias zonas de información de forma simultánea.

**¿Cuáles media queries utilizó y por qué seleccionó esos breakpoints?**
Se usaron `min-width: 601px` (tableta) y `min-width: 1024px` (escritorio), siguiendo
la referencia orientativa de la consigna, ya que cubren bien los anchos típicos de
teléfonos, tabletas y monitores de escritorio.

**¿Cuáles unidades relativas utilizó?**
Se usó `rem` para tipografía y espaciados (a través de las variables CSS), `%` y `fr`
para las columnas de Grid, y unidades relativas de flexbox (`flex: 1 1 auto`, etc.)
para el ancho de los elementos, evitando depender de píxeles fijos.

**¿Para qué sirven las variables CSS que definió?**
Las variables (`--color-primario`, `--color-secundario`, `--color-fondo`,
`--color-texto`, `--espaciado-xs/sm/md/lg`, `--radio-borde`, entre otras) centralizan
la paleta visual y el sistema de espaciado de cada caso. Esto permitió, por ejemplo,
cambiar toda la paleta de colores del Caso 2 editando solo dos líneas, sin tocar el
resto del CSS.

## Resumen de commits
## Resumen de commits

| # | Fecha | Hash | Mensaje | Caso | Cambio |
|---|------------|---------|---------------------------------------------------------------------------------------------------------------------|--------|------------------------------------------------|
| 1 | 2026-09-14 | 4ea0d09 | Initial commit | Ambos | Commit inicial generado por GitHub |
| 2 | 2026-09-14 | 59940e6 | Crear estructura base del repositorio con carpetas caso1 y caso2 | Ambos | Estructura de carpetas y archivos vacíos |
| 3 | 2026-09-14 | 9b04cb5 | Agregar estructura HTML semantica completa del Caso 1... | Caso 1 | HTML: header, nav, main con todas las secciones |
| 4 | 2026-09-14 | a7f92ca | Definir variables CSS y reset basico del Caso 1 | Caso 1 | Variables CSS y reset |
| 5 | 2026-09-14 | c3e36fa | Agregar estilos del header y navegacion con Flexbox y position sticky | Caso 1 | Header y nav con Flexbox y sticky |
| 6 | 2026-09-14 | 04418df | Agregar estilos de indicadores del resumen y tarjetas de misiones con Flexbox | Caso 1 | Indicadores y tarjetas de misiones |
| 7 | 2026-09-14 | 4320865 | Agregar estilos de equipos, alertas con jerarquia visual y agenda | Caso 1 | Equipos, alertas y agenda |
| 8 | 2026-09-14 | a2d67c2 | Implementar CSS Grid para escritorio y ajustes de tablet con media queries mobile-first | Caso 1 | Grid de escritorio y media queries |
| 9 | 2026-09-15 | 533a72e | Agregar estructura HTML semantica completa del Caso 2... | Caso 2 | HTML: header, nav, main con todas las secciones |
| 10 | 2026-09-15 | bb2c344 | Definir variables CSS, reset y estilos base de header y navegacion sticky del Caso 2 | Caso 2 | Variables, reset, header y nav sticky |
| 11 | 2026-09-15 | 49233af | Agregar estilos de la seccion Ahora con position absolute para la etiqueta destacada | Caso 2 | Seccion Ahora con position absolute |
| 12 | 2026-09-15 | 372bd33 | Agregar estilos de proximas actividades, escenarios, cambios y servicios del Caso 2 | Caso 2 | Proximas, escenarios, cambios y servicios |
| 13 | 2026-09-15 | 1d49338 | Ajustar paleta de colores del Caso 2: celeste claro y amarillo crema con buen contraste | Caso 2 | Ajuste de paleta de colores |
| 14 | 2026-09-16 | (pendiente) | Agregar README.md completo con decisiones de diseño y tabla de commits | Ambos | Documentación completa del repositorio |