# Radar del Ecosistema Creativo

Actividad educativa gamificada de un solo archivo HTML para la sesión **"Mercado y Rubro: Vigilancia Tecnológica e Innovación Abierta"** (Unidad 4: El ecosistema de innovación local). Construida bajo el modelo pedagógico IUTPC con tres juegos interactivos y mecánica de refuerzo del aprendizaje.

**Stack:** HTML5 + CSS3 + JavaScript vanilla. Sin frameworks, sin build, sin servidor, sin dependencias instalables. Las fuentes (Google Fonts) cargan por CDN con fallback a `system-ui`.

---

## Características técnicas

- **Archivo único autocontenido** (`radar-ecosistema-idc-v2.html`, ~138 KB). Todo el CSS, JS y los assets están embebidos.
- **Logo IDC embebido en base64** (data URI JPEG, sin archivos de imagen externos).
- **Estado 100% en memoria.** No usa `localStorage` ni `sessionStorage`; al recargar, la sesión se reinicia.
- **Funciona offline** y por `file://` (doble clic), salvo la descarga de fuentes web.
- **Responsive** y con soporte de interacción táctil (fallback tap-to-place donde el drag nativo no dispara en móvil).
- **Impresión** del informe final vía `@media print`.

---

## Estructura del proyecto

```
.
├── radar-ecosistema-idc-v2.html   # Aplicación completa (único entregable)
└── README.md
```

Internamente el HTML se organiza así:

```
radar-ecosistema-idc-v2.html
├── <head>
│   ├── Google Fonts (Poppins + Inter)
│   └── <style>  — tokens IDC, layout, estilos de los 3 juegos
└── <body>
    ├── #scrim          — pantalla de carga
    ├── #bgCanvas       — radar de fondo animado
    ├── #sparkle-layer  — partículas de celebración
    ├── header.topbar   — HUD (puntos, rango, racha) + barra de fases
    ├── main
    │   ├── #p-registro        — registro de equipo
    │   ├── #p-presentacion    — briefing
    │   ├── #p-inicio          — JUEGO 1: Clasificador (drag)
    │   ├── #p-utilidad        — JUEGO 2: Anagrama
    │   ├── #p-transformacion  — JUEGO 3: Simulador Radar (drag) + reto vinculación
    │   ├── #p-practica         — directorio editable + pitch + rúbrica
    │   └── #p-cierre           — informe, insignias, dos estrellas y un deseo
    ├── footer.foot
    └── <script>  — lógica de estado, navegación y los 3 juegos
```

---

## Instalación y ejecución

No requiere instalación. Tres formas de usarlo:

**1. Local (doble clic)**
```
Abrir radar-ecosistema-idc-v2.html en cualquier navegador moderno.
```

**2. Servidor local (recomendado para pruebas)**
```bash
python3 -m http.server 8000
# luego abrir http://localhost:8000/radar-ecosistema-idc-v2.html
```

**3. GitHub Pages**
```bash
git init
git add radar-ecosistema-idc-v2.html README.md
git commit -m "Radar del Ecosistema Creativo"
git branch -M main
git remote add origin https://github.com/USUARIO/REPO.git
git push -u origin main
```
Luego, en **Settings → Pages**, selecciona la rama `main` y la carpeta raíz (`/root`). Opcional: renombra el archivo a `index.html` para que cargue en la URL base del sitio.

---

## Los tres juegos

| Fase IUTPC | Juego | Mecánica | Concepto reforzado |
|---|---|---|---|
| Inicio | **Clasificador** | Arrastrar casos a dos columnas | Innovación incremental vs. disruptiva |
| Utilidad | **Anagrama** | Descifrar términos desordenados | Vocabulario clave (7 términos) |
| Transformación | **Simulador Radar** | Arrastrar actores a su agente | Sistema de Innovación Regional |

Cada error abre un panel de **refuerzo del aprendizaje** con cuatro elementos: pista, dato, analogía y una pregunta de refuerzo (+3 pts). Los aciertos suman puntos con bonus por racha, desbloquean insignias y disparan partículas.

> **Nota de diseño:** el panel de refuerzo orienta y bonifica, pero **no bloquea el avance** (no obliga a acertar la pregunta de refuerzo para continuar). La skill de referencia contempla el bloqueo estricto como opción; aquí se priorizó el ritmo de aula presencial.

---

## Personalización

| Qué cambiar | Dónde, dentro de `<script>` |
|---|---|
| Casos del clasificador | array `CASOS_CLAS` |
| Términos del anagrama (palabra, pista, definición, refuerzo) | array `TERMINOS` |
| Actores y agentes del radar | arrays `ACTORES` y `AGENTES` |
| Reto de vinculación | array `VINCULOS` |
| Rúbrica y checklist | arrays `RUBRICA` y `CHECKLIST` |
| Rangos por puntaje | array `RANGOS` |

Diseño visual (dentro de `<style>`, en `:root`):

```css
--naranja:#f3a100;  /* IDC */
--azul:#0072b9;     /* IDC */
--gris:#555553;     /* IDC */
--gris2:#545452;    /* IDC */
```

Para reemplazar el logo IDC, sustituye las tres ocurrencias de la cadena base64 `data:image/jpeg;base64,...` por tu propio data URI.

---

## Compatibilidad

- Chrome, Edge, Firefox y Safari recientes.
- El arrastre (drag-and-drop) usa la API nativa de HTML5; en navegadores móviles donde no dispara, hay un fallback de **tocar el elemento y luego el destino**.
- Para arrastre fluido garantizado en móvil se requeriría reescribir con Pointer Events (no incluido para mantener el archivo libre de dependencias).

---

## Validación

El JavaScript embebido se validó con `node --check`. No produce errores de sintaxis.

---

## Créditos

**Mg. Mario Quiroz Martínez**
Unidad didáctica: Investigación e Innovación Tecnológica
Instituto de Diseño y Comunicación (IDC) · 2026
