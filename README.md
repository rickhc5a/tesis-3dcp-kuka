# Tesis: Impresión 3D de Concreto con Robot KUKA — SIMPLE
**Sincronización Bomba-Robot para Impresión 3D de Concreto (3DCP)**  
Universidad Peruana de Ciencias Aplicadas (UPC) — Ingeniería Mecatrónica  
Autor: Gianpiero Rick Huaricapcha  
Año: 2026

---

## Descripción

Este repositorio contiene todo el material técnico de la tesis de pregrado sobre
impresión 3D de concreto (3DCP) con un brazo robótico KUKA industrial.

El sistema integra:
- Robot **KUKA** con programación KRL
- **Bomba de mortero** BF-990 (1800W, caudal 1–10 L/min)
- Pipeline de generación de trayectorias en **Grasshopper + KUKA|prc**
- Soporte para impresión **planar y no-planar**

---

## Estructura del repositorio

```
tesis-3dcp-kuka/
├── 01_grasshopper/     # Definiciones GH: generación de trayectorias
├── 02_krl/             # Código KRL para el controlador KUKA
├── 03_gcode/           # G-code fuente (logo, perfiles)
├── 04_cad/             # Modelos 3D (nozzle, bloque de ensayo)
├── 05_latex/           # Documento de tesis en LaTeX
├── 06_datos/           # Datos de calibración y ensayos
└── 07_docs/            # Poster, fotos, presentaciones
```

---

## Flujo del sistema

```
G-code / Geometría Rhino
        │
        ▼
  Grasshopper (Python script)
  - Parseo de G-code
  - Generación de planos
  - Control de capas (planar / non-planar)
        │
        ▼
  KUKA|prc
  - Simulación de trayectoria
  - Export .src + .dat
        │
        ▼
  Controlador KUKA (KRC)
  - Secuencia de purga con HALT manual
  - Sincronización bomba-robot
  - Impresión continua sin paradas (C_DIS)
```

---

## Parámetros clave del sistema

| Parámetro | Valor | Notas |
|-----------|-------|-------|
| Velocidad de impresión | 0.05 m/s | Calibrar según caudal |
| Tiempo de purga agua | 12 s | Manguera 3/4", 2.5 m |
| Tiempo de transición | 8 s | Agua + concreto (impurezas) |
| Altura de capa | 20 mm | Ajustar según boquilla |
| Capas planas base | 2 | Antes de activar non-planar |
| Altura de clearance | 10 mm | Sobre superficie del bloque |

---

## Protocolo de operación

1. Ejecutar definición GH → verificar simulación en KUKA|prc
2. Exportar `.src` → copiar al controlador KUKA vía USB
3. Posicionar robot en HOME manualmente
4. Ejecutar programa:
   - Pantalla muestra `"ENCIENDE LA BOMBA DE AGUA"` → encender → **START**
   - Espera purga (12 s automático)
   - Pantalla muestra `"CAMBIA A CONCRETO"` → cambiar → **START**
   - Espera transición (8 s automático)
   - Pantalla muestra `"VERIFICA FLUJO"` → verificar → **START**
   - Robot imprime logo de forma continua
   - Pantalla muestra `"APAGA LA BOMBA"` → apagar → **START**

---

## Dependencias

### Software
- [Rhinoceros 3D](https://www.rhino3d.com/) + Grasshopper
- [KUKA|prc](https://www.robotsinarchitecture.org/kuka-prc) (Community Version)
- [KUKA.Sim](https://www.kuka.com/) 4.1 (simulación offline)
- Python 3.x (IronPython en GH)

### Hardware
- Robot KUKA (modelo: ___)
- Bomba de mortero SC BF-990
- Manguera 3/4" × 2.5 m
- Boquilla de ___ mm

---

## Publicaciones relacionadas

- Paper CACRE 2026: *"Pump-Robot Synchronization for 3D Concrete Printing with Eco-friendly Nozzle"*
- Estancia KTH Royal Institute of Technology — NanoREPU Program (2025)

---

## Cómo citar

```bibtex
@thesis{huaricapcha2026,
  author  = {Huaricapcha, Gianpiero Rick},
  title   = {Sincronización Bomba-Robot para Impresión 3D de Concreto},
  school  = {Universidad Peruana de Ciencias Aplicadas},
  year    = {2026},
  type    = {Tesis de pregrado}
}
```

---

## Contacto

Gianpiero Rick Huaricapcha  
Joaquin Velarde Yaranga
Camila Sulen
Universidad Peruana de Ciencias Aplicadas - Lima, Perú
