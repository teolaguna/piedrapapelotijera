# Manual de Usuario — Mini Juego Piedra, Papel o Tijera v1.0.0

**Materia:** Laboratorio de Programación — EEST N.º 1 "Eduardo Ader"
**Actividad 7 — Persistencia de datos (struct + fstream) — Modalidad individual**
**Versión:** v1.0.0 — Fecha: 16/10/2026

## 1. Introducción

Este manual explica cómo instalar, ejecutar y jugar al Mini Juego
Piedra, Papel o Tijera contra la IA, y cómo consultar el historial
de partidas guardado en disco.

No se requieren conocimientos de programación para usar el juego.

## 2. Requisitos

- PC con Windows 10/11.
- Opción A (recomendada en el aula): compilador `g++` (MinGW) y Visual Studio Code.
- Opción B (si no hay permisos de instalación): navegador web para usar OnlineGDB.
- Archivos del proyecto: `src/main.cpp` y carpeta `src/` con permiso de escritura
  (para generar `historial_partidas.txt`).

## 3. Instalación / Preparación

1. Copiar la carpeta `piedrapapelotijera/` a un lugar con permiso de escritura
   (por ejemplo, Escritorio o Documentos).
2. Abrir la carpeta en VS Code.
3. Verificar que existe `src/main.cpp`.
4. Abrir una terminal PowerShell en la raíz del proyecto
   (Terminal > Nueva terminal en VS Code).

## 4. Compilación y ejecución

```powershell
# Compilar (habilita C++11)
g++ -std=c++11 src/main.cpp -o src/piedrapapelotijera.exe

# Ejecutar
.\src\piedrapapelotijera.exe
```

Si aparece un aviso de permisos en la PC de la escuela, usar OnlineGDB:
pegar el contenido de `src/main.cpp`, pulsar Run, probar y luego
descargar los archivos a `src/`.

## 5. Cómo jugar (paso a paso)

Al iniciar verá el encabezado `LPR 2026 - ACTIVIDAD 7` y el menú:

```text
--- MENU PRINCIPAL DE JUEGO Y PERSISTENCIA ---
1. Jugar Partida (Piedra, Papel o Tijera)
2. Ver Historial de Partidas Guardadas en Disco (.txt)
3. Salir del Sistema
Ingrese una opcion (1-3):
```

### Opción 1 — Jugar

1. Escriba `1` y pulse Enter.
2. Ingrese su Nombre / Nickname y pulse Enter
   (puede contener espacios, por ejemplo `Teo Laguna`).
3. Elija jugada: `1` Piedra, `2` Papel, `3` Tijera.
4. El programa muestra su elección, la elección de la IA y el resultado:
   `Victoria`, `Derrota` o `Empate`.
5. Verá el mensaje `[DISCO] Partida resguardada con exito...`.
   La partida ya quedó guardada en `src/historial_partidas.txt`.

Reglas: Piedra vence a Tijera, Tijera vence a Papel, Papel vence a Piedra.
Iguales = Empate.

### Opción 2 — Ver historial

1. Escriba `2` y pulse Enter.
2. Se lista cada línea del archivo, por ejemplo:
   `Partida #1 | Jugador: Ana | Piedra vs Tijera | Resultado: Victoria`
3. Al final indica el total de registros leídos desde disco.
4. Si aún no jugó ninguna partida verá:
   `[AVISO] Aun no existen partidas guardadas en disco.`

Prueba de persistencia: juegue una partida, cierre la ventana,
vuelva a abrir el `.exe` y elija la opción 2. El historial anterior
sigue apareciendo porque está en el disco, no en la RAM.

### Opción 3 — Salir

Escriba `3` y pulse Enter. Verá
`[SISTEMA] Saliendo del programa... Datos resguardados en disco.`

## 6. Dónde está el archivo guardado

`src/historial_partidas.txt`, una línea por partida en formato CSV:

```text
idPartida,jugador,eleccionJugador,eleccionIA,resultado
1,Ana,Piedra,Tijera,Victoria
```

Puede abrirlo con Bloc de notas. No lo edite mientras el juego está abierto.
Cada partida nueva se agrega al final sin borrar las anteriores.

## 7. Solución de problemas frecuentes

| Problema | Causa / Solución |
|---|---|
| No se crea `historial_partidas.txt` | Es normal hasta jugar la primera partida (Opción 1). Revise la carpeta `src/`. |
| Se saltea el nombre del jugador | Falta `cin.ignore()` antes de `getline()`. Use el `main.cpp` provisto sin modificar esa línea. |
| Opción inválida | Ingrese solo `1`, `2` o `3`. |
| Error de permisos al compilar | Use `g++ -std=c++11` o pruebe en OnlineGDB. |
| El historial sale vacío | El archivo existe pero no tiene líneas. Juegue al menos una partida. |
| Nombres con comas | Evite comas en el nickname porque el archivo usa comas como separador. |

## 8. Datos del estudiante (completar)

- Nombre y Apellido: Teo Laguna
- Curso: 5° 3° Grupo: A / B
- Fecha: 16/10/2026

---
*Manual de usuario v1.0.0 — Actividad 7 LPR 2026.*
