# 🎮 Mini Juego "Piedra, Papel o Tijera" con Persistencia de Datos (struct + fstream)

**Materia:** Laboratorio de Programación (LPR) — 5° Año 3° Grupos A-B
**Institución:** EEST N.º 1 – "Eduardo Ader", Vicente López
**Actividad 7 — 2° Cuatrimestre 2026**
**Modalidad:** Individual

## 📝 Descripción

Mini juego de Piedra, Papel o Tijera contra la IA de la consola, con registro
automático de cada partida en una estructura `struct Partida` y persistencia
en disco mediante `<fstream>` en el archivo `src/historial_partidas.txt`
(formato CSV, modo `ios::app`).

## 👤 Integrante (modalidad individual)

- **Nombre y Apellido:** Teo Laguna
- **Curso:** 5° Año 3° Grupo: A / B
- **Profesor:** Mansilla Muñoz York Elías y Yamil Ganduglia
- **Fecha de entrega:** 16 de Octubre de 2026

## 📁 Estructura del repositorio

```text
piedrapapelotijera/
├── .gitattributes
├── .gitignore
├── LICENSE
├── README.md
├── docs/
│   ├── InformeEEST1_LPR2026_ACT07_Individual_TeoLaguna_Informe_v1.0.0.pdf
│   ├── CHANGELOG.md
│   └── manuales/
│       ├── manual_programador_v1.0.0.md
│       ├── manual_programador_v1.0.0.pdf
│       ├── manual_usuario_v1.0.0.md
│       └── manual_usuario_v1.0.0.pdf
├── src/
│   ├── main.cpp
│   ├── historial_partidas.txt
│   └── piedrapapelotijera.exe (generado al compilar, no se versiona)
└── capturas/
    ├── jugada_consola.png
    └── archivo_disco.png
```

> `capturas/` contiene las evidencias de ejecución: `jugada_consola.png`
> (menú y partida jugada) y `archivo_disco.png` (archivo `.txt` abierto).

## ⚙️ Compilación y ejecución (PowerShell en VS Code, Windows 10/11)

```powershell
# 1. Compilación con estándar C++11
g++ -std=c++11 src/main.cpp -o src/piedrapapelotijera.exe

# 2. Ejecución directa
.\src\piedrapapelotijera.exe
```

Alternativa sin compilador local: pegar `src/main.cpp` en OnlineGDB,
ejecutar, descargar y ubicar los archivos en esta estructura.

## 🎮 Uso rápido

1. Opción `1`: jugar una partida (ingresar nombre, elegir 1-3).
   Se guarda automáticamente en `src/historial_partidas.txt`.
2. Opción `2`: ver el historial recuperado desde disco.
3. Opción `3`: salir (los datos quedan resguardados en disco).

## 📚 Documentación

- `docs/`: informe APA v7 (PDF) con cuestionario técnico respondido.
- `docs/manuales/`: manual de usuario y manual del programador (MD + PDF).
- `docs/CHANGELOG.md`: historial de versiones.

## 📄 Licencia

Licencia MIT escolar. Ver archivo `LICENSE`.
