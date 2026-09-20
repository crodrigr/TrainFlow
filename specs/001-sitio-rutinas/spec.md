# Especificación: Sitio web de rutinas de entrenamiento

**Rama**: `001-sitio-rutinas`
**Estado**: Borrador
**Idioma del contenido**: Español

## Resumen

Un sitio web estático, pensado para usarse desde el celular, donde se puedan
consultar varias rutinas de entrenamiento. La primera rutina es la
"Rutina Avanzada 5 días" (barra pull-up + TRX, mancuernas solo para bíceps),
que ya existe en `1-runtina/`. El sitio debe permitir agregar más rutinas
después sin rehacer nada.

**Restricción de tecnología dada por el usuario**: solo HTML y CSS, página
estática. Sin JavaScript, sin backend, sin base de datos.

## Historias de usuario

### HU1 — Ver una rutina en el celular (Prioridad: P1)

Como persona que entrena, abro el sitio en mi celular en el gimnasio o en casa
y leo los ejercicios del día sin hacer zoom ni desplazarme de lado.

**Por qué P1**: es el uso principal; si esto no funciona, el sitio no sirve.

**Pruebas de aceptación**:
1. **Dado** un celular con pantalla de 360 px de ancho, **cuando** abro una
   rutina, **entonces** todo el contenido se lee sin zoom y sin scroll horizontal.
2. **Dado** el detalle de un día, **cuando** lo miro, **entonces** cada ejercicio
   muestra nombre, series x repeticiones (o tiempo) y su nota si la tiene.
3. **Dado** que estoy entrenando con las manos ocupadas, **cuando** toco un
   enlace o botón, **entonces** el objetivo táctil es lo bastante grande para
   pulsarlo sin error.

### HU2 — Elegir entre varias rutinas (Prioridad: P1)

Como usuario, veo una página de inicio con la lista de rutinas disponibles y
entro a la que quiero.

**Pruebas de aceptación**:
1. **Dado** que abro la página de inicio, **cuando** carga, **entonces** veo una
   tarjeta por rutina con nombre, número de días y objetivo.
2. **Dado** una tarjeta, **cuando** la toco, **entonces** llego a esa rutina.
3. **Dado** cualquier página de una rutina, **cuando** quiero volver,
   **entonces** hay un enlace visible al inicio.

### HU3 — Navegar entre los días de una rutina (Prioridad: P1)

Como usuario, salto directo al día que me toca (Lunes, Martes, etc.) sin
recorrer toda la página.

**Pruebas de aceptación**:
1. **Dado** una rutina de 5 días, **cuando** la abro, **entonces** veo un menú
   con los 5 días que lleva a cada sección.
2. **Dado** que estoy en un día, **cuando** quiero cambiar de día, **entonces**
   puedo hacerlo sin volver al inicio de la página.

### HU4 — Consultar reglas, progresión y notas (Prioridad: P2)

Como usuario, consulto las reglas generales (calentamiento, RIR, descansos), la
progresión de 8 semanas y las notas de la rutina.

**Pruebas de aceptación**:
1. **Dado** la rutina "Avanzada 5 días", **cuando** busco las reglas o la
   progresión, **entonces** están en secciones propias y enlazadas desde el menú.
2. **Dado** contenido largo, **cuando** abro la página, **entonces** las
   secciones secundarias pueden estar colapsadas y expandirse al tocarlas.

### HU5 — Agregar una rutina nueva (Prioridad: P2)

Como autor del sitio, agrego otra rutina copiando una plantilla, sin tocar el
diseño ni el resto de rutinas.

**Pruebas de aceptación**:
1. **Dado** la plantilla de rutina, **cuando** la copio y cambio el contenido,
   **entonces** la nueva rutina tiene el mismo aspecto que las demás.
2. **Dado** una rutina nueva, **cuando** agrego una tarjeta en el inicio,
   **entonces** ya se puede acceder a ella. No hay más pasos.

### HU6 — Ver el póster de la rutina (Prioridad: P3)

Como usuario, quiero abrir el póster ilustrado de la rutina como imagen
completa, aparte del contenido en texto.

**Pruebas de aceptación**:
1. **Dado** una rutina con póster, **cuando** toco el enlace al póster,
   **entonces** se abre la imagen, sin cargarla en la página de lectura.

## Requisitos funcionales

- **RF-01**: El sitio se compone solo de archivos HTML y CSS estáticos, sin
  JavaScript y sin dependencias externas obligatorias.
- **RF-02**: Existe una página de inicio con la lista de rutinas.
- **RF-03**: Cada rutina tiene su propia página, con una sección por día,
  enlazadas desde un menú de días.
- **RF-04**: Cada ejercicio muestra nombre, series, repeticiones o tiempo, y
  notas opcionales (por ejemplo, "por lado", "por pierna", la progresión del
  front lever).
- **RF-05**: Los ejercicios se agrupan por bloque dentro del día (por ejemplo
  Pecho, Hombros TRX, Tríceps, Core, Habilidades, Finisher opcional).
- **RF-06**: Cada rutina puede incluir secciones generales: reglas, progresión
  por semanas, uso del equipo y consejos.
- **RF-07**: El diseño se adapta a pantallas desde 320 px hasta escritorio
  (mobile-first).
- **RF-08**: Los colores, tipografías y espaciados están definidos en una sola
  hoja de estilos compartida por todas las páginas.
- **RF-09**: Existe una plantilla de rutina para crear otras nuevas.
- **RF-10**: Respeta el modo claro y oscuro del dispositivo (`prefers-color-scheme`).
- **RF-11**: Al imprimir una rutina, la salida es legible y sin menús.

## Fuera de alcance

Estas funciones necesitan JavaScript o un servidor. Quedan fuera mientras el
sitio sea solo HTML y CSS:

- Resaltar automáticamente "el día de hoy".
- Registrar pesos, repeticiones o progreso.
- Cuentas de usuario y sincronización entre dispositivos.
- Búsqueda y filtros dinámicos.
- Funcionamiento sin conexión (requiere service worker).
- Temporizador de descanso.

## Casos límite

- Pantalla muy angosta (320 px): las tablas o listas de ejercicios no deben
  desbordar.
- Nombres largos de ejercicio ("Peso muerto a una pierna asistido con TRX")
  deben ajustarse en varias líneas.
- Conexión lenta: la página de lectura no debe cargar imágenes pesadas. El
  póster actual pesa unos 2,2 MB, así que debe abrirse solo cuando se pide.
- Un día con muchos ejercicios (el miércoles tiene 12) sigue siendo fácil de
  recorrer.
- Ejercicios opcionales (finisher) deben distinguirse de los obligatorios.

## Entidades de contenido

- **Rutina**: nombre, objetivo, equipo, número de días, secciones generales.
- **Día**: nombre (Lunes…), enfoque (Pull, Push, Piernas…), lista de bloques.
- **Bloque**: título (Pecho, Core…) y lista de ejercicios.
- **Ejercicio**: nombre, series, repeticiones o tiempo, nota opcional.

## Criterios de éxito

- **CE-01**: Una rutina completa se lee en un celular de 360 px sin zoom y sin
  scroll horizontal.
- **CE-02**: Llegar a cualquier día desde el inicio toma como máximo 2 toques.
- **CE-03**: Agregar una rutina nueva requiere crear un archivo HTML y añadir
  una tarjeta en el inicio.
- **CE-04**: La página de una rutina pesa menos de 200 KB sin contar el póster.
- **CE-05**: Contraste de texto AA (WCAG) en modo claro y oscuro.
- **CE-06**: Las páginas pasan la validación de HTML sin errores.

## Supuestos

- Se publicará en un hosting estático (por ejemplo GitHub Pages).
- El público es una sola persona o un grupo pequeño; no se necesita
  administración de contenido.
- El contenido de cada rutina se toma de su archivo `.txt` en `1-runtina/`
  (fuente del contenido) y la imagen de esa carpeta sirve de referencia visual
  (un color por día). Para la primera rutina:
  `1-runtina/rutina_5_dias_TRX_hombros_mancuernas_biceps.txt`.

## Preguntas abiertas

1. **[POR ACLARAR]** ¿Cuántas rutinas y cuáles habrá al inicio, además de la
   "Avanzada 5 días"?
2. **[POR ACLARAR]** ¿Dónde se publicará (GitHub Pages, Netlify, otro)? Los
   enlaces del sitio son relativos, así que funciona en cualquier hosting
   estático, incluso bajo una subcarpeta.

**Resuelta**: el póster se incluye como versión liviana (`img/avanzada-5-dias-poster.webp`,
287 KB frente a 2,2 MB del PNG original) y solo se abre desde un botón.
