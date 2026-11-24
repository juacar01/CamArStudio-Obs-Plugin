# CamAr Studio OBS — Beauty Filter Plugin

Plugin nativo de **belleza y retoque facial en tiempo real** para **OBS Studio** (Windows 64-bit), construido en **Rust + Direct3D 11 + DirectML GPU**.

> **Descargas oficiales (Instalador `.exe` y Portable `.zip`):**  
> [GitHub Releases — CamArStudio-Obs-Plugin](https://github.com/juacar01/CamArStudio-Obs-Plugin/releases)  
> **Documentación web (GitHub Pages):**  
> [juacar01.github.io/CamArStudio-Obs-Plugin](https://juacar01.github.io/CamArStudio-Obs-Plugin/)

---

## ✨ Características Principales

- **Tracking IA de 0 retraso:** Inferencia síncrona por frame con modelos ONNX (`FaceMesh` 478 puntos con iris, `face_blendshapes`, `UltraFace` y segmentación multiclase) acelerada por **DirectML GPU**.
- **Aislamiento total de dependencias:** Usa su propia librería privada `camar_onnxruntime.dll` + `DirectML.dll` dentro de `obs-plugins/64bit/`, sin modificar archivos originales de OBS ni chocar con otros plugins (como `obs-backgroundremoval`).
- **Color 1:1 Passthrough:** Respeta intacta la gestión de color y gamma de OBS Studio para que puedas encadenar tus propios filtros de color encima sin distorsiones.
- **Soporte nativo para cámaras verticales (`90° / 180° / 270°`):** Detección automática de la orientación del rostro con pre-rotación y des-rotación en VRAM antes del tracker IA (sin configuración manual).
- **Shaders DXBC precompilados & arranque no bloqueante:** Los shaders HLSL van precompilados en bytecode binario dentro de `camar_obs.dll` y los motores IA se inicializan en segundo plano mostrando un popup animado con el logo de CamAr.

---

## 🎛️ Funcionalidades del Filtro (`CamAr Studio Beauty Filter`)

### 1. 💆‍♀️ Rostro & Piel
- **Suavizado de Piel (%)** — Suavizado bilateral guiado por malla facial protegiendo ojos, cejas, labios y cabello.
- **Blanqueamiento Radiante (%)** — Aclarado fotométrico natural del rostro.
- **Corrector / Imperfecciones (%)**, **Suavizar Arrugas (%)**, **Reducir Ojeras (%)**, **Reducir Bolsas (%)**.
- **Claridad de Piel (%)** e **Iluminación Facial 3D (%)**.
- **Base / Tez:** Selector de tono (`Porcelana`, `Marfil`, `Beige Cálido`, `Bronceado Natural`, `Miel`, `Caramelo`, `Espresso`) + **Intensidad de Base (%)**.
- **Contorno Facial (%)**, **Armonía Facial (%)**, **Afinado de Rostro (%)**, **Afinado de Nariz (%)** y **Relieve de Nariz (%)**.

### 2. 👁️ Ojos, Cejas & Mirada
- **Morfología ocular:** Agrandar Ojos (%), Redondear Ojos (%), Forma de Ojo (`Automático`, `Almendrado`, `Foxy`, `Asiático`, `Doe / Muñeca`, `Encapotado`).
- **Pupilentes 3D:** 7 colores (`Verde Esmeralda`, `Avellana Cálido`, `Miel Claro`, `Gris Perla`, `Azul Hielo`, `Zafiro Profundo`, `Violeta`) + Opacidad (%), Brillo Ocular / Esclera (%) y **Encuadre de Mirada (%)**.
- **Aclarar Ojos (%)** y **Definición de Ojos (%)**.
- **Pestañas (%)**, **Delineado (%)**, **Sombras** (intensidad, color y estilo) y **Cejas** (intensidad, color, estilo y Elevar Cejas %).

### 3. 💋 Boca, Dientes & Barba
- **Labial 3D:** Intensidad (%), 8 tonos (`Rojo Clásico`, `Rosa Natural`, `Nude Cálido`, `Coral Durazno`, `Rosa Suave`, `Ciruela Intenso`, `Vino Borgoña`, `Coral Suave`), Definición (%) y Volumen (%).
- **Blanqueamiento Dental (%)** con detección anatómica de esmalte y estabilización temporal.
- **Realce de Barba (%)** y selector de tono (`Natural`, `Negro`, `Castaño Oscuro`, `Castaño Medio`).

### 4. 🎬 Fondo, IA & Rendimiento
- **Desenfoque de Fondo Bokeh (%)** con segmentación de silueta en GPU.
- **Iluminación Inteligente (AI Lighting)** y **Reducción de Ruido Bilateral**.
- **Perfil de Rendimiento:** `Equilibrado (Automático)`, `Calidad Máxima`, `Máximo Rendimiento (FPS)`.

---

## 📦 Instalación

### Opción A: Instalador Oficial (`.exe`) — Recomendado
1. Descarga `CamAr-OBS-vX.Y.Z-Setup.exe` desde [Releases](https://github.com/juacar01/CamArStudio-Obs-Plugin/releases).
2. Cierra **OBS Studio** y ejecuta el instalador.
3. El asistente detectará automáticamente tu carpeta de OBS Studio (o te permitirá elegir una instalación portable con **Examinar...**).
4. Abre OBS Studio, haz clic derecho en tu fuente de cámara/escena → **Filtros** → **+** en *Filtros de efecto* → **`CamAr Studio Beauty Filter`**.

### Opción B: Paquete Portable (`.zip`)
1. Descarga `CamAr-OBS-vX.Y.Z-Portable.zip`.
2. Descomprime su contenido (`obs-plugins/` y `data/`) directamente en la carpeta raíz de tu OBS Studio.

---

## ⚙️ Configuración Rápida Recomendada en OBS

- **Cámara vertical física:** Si tu cámara entra acostada (`1920×1080`) al filtro antes de rotarla en el lienzo vertical de OBS, el filtro detecta automáticamente la orientación (`0° / 90° / 180° / 270°`) y la corrige; no necesitas configurar nada.
- **Orden de filtros:** Coloca `CamAr Studio Beauty Filter` **primero** en la pila de filtros y añade después tus LUTs o filtros de corrección de color de OBS si los necesitas.

---

## 💻 Requisitos del Sistema

- **SO:** Windows 10 / Windows 11 (64-bit)
- **Software:** OBS Studio 30.x o superior (64-bit, renderizador Direct3D 11)
- **GPU:** Compatible con Direct3D 11 y DirectML (NVIDIA, AMD o Intel)
