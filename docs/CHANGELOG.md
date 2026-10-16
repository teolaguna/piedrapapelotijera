# CHANGELOG — Mini Juego Piedra, Papel o Tijera

Historial de versiones del software (formato basado en Keep a Changelog).

## [v1.0.0] — 2026-10-16

### Agregado
- `src/main.cpp`: programa principal con `struct Partida`, menú (jugar / ver historial / salir), IA aleatoria con `rand()`, persistencia con `ofstream` (`ios::app`) y lectura con `ifstream`.
- `src/historial_partidas.txt`: archivo de persistencia generado (formato CSV: `idPartida,jugador,eleccionJugador,eleccionIA,resultado`).
- `docs/InformeEEST1_LPR2026_ACT07_Individual_TeoLaguna_Informe_v1.0.0.pdf`: informe APA v7 individual con cuestionario técnico respondido.
- `docs/manuales/manual_usuario_v1.0.0.md` y `.pdf`: manual de usuario.
- `docs/manuales/manual_programador_v1.0.0.md` y `.pdf`: manual del programador.
- `.gitattributes`: normalización de finales de línea.
- `.gitignore`: exclusiones (`*.exe`, `*.out`, `.vscode/`).
- `README.md`: portada del proyecto (modalidad individual).
- `LICENSE`: licencia MIT escolar.
- `capturas/`: evidencias de ejecución (`jugada_consola.png` y `archivo_disco.png`).

### Notas
- Modalidad individual (no P.I.A. grupal): se desarrolla el juego tal cual lo provisto en la Actividad 7.
- Compilación verificada con `g++ -std=c++11 src/main.cpp -o src/piedrapapelotijera.exe`.
