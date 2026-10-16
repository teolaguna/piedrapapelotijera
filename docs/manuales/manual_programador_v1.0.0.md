# Manual del Programador — Mini Juego Piedra, Papel o Tijera v1.0.0

**Materia:** Laboratorio de Programación — EEST N.º 1 "Eduardo Ader"
**Actividad 7 — struct + fstream — Modalidad individual**
**Versión:** v1.0.0 — Fecha: 16/10/2026
**Archivo:** `src/main.cpp` — Estándar: C++11

## 1. Alcance y arquitectura

Programa de consola en un único archivo `src/main.cpp`, paradigma
estructurado/modular, sin clases ni librerías externas.
Persistencia en archivo de texto CSV `src/historial_partidas.txt`.

Módulos:

```text
main() -> jugarPartida(contadorID) -> guardarEnDisco(p)
main() -> leerHistorialDisco()
```

- `main`: inicializa `srand(time(0))`, menú `do-while (opcion != 3)`.
- `jugarPartida`: entrada, lógica del juego, delega el guardado.
- `guardarEnDisco`: escritura `ofstream` en modo `ios::app`.
- `leerHistorialDisco`: lectura `ifstream` con `getline(..., ',')`.

## 2. Estructura de datos

```cpp
struct Partida {
    int idPartida;          // correlativo en la sesión (1, 2, 3...)
    string jugador;         // nickname (puede tener espacios)
    string eleccionJugador; // "Piedra" | "Papel" | "Tijera"
    string eleccionIA;      // "Piedra" | "Papel" | "Tijera"
    string resultado;       // "Victoria" | "Derrota" | "Empate"
};
```

Ventajas frente a 5 variables sueltas: una sola entidad que se pasa
por referencia (`const Partida&`), código más legible, fácil de
extender (agregar fecha, puntaje) y mapeo 1:1 con una línea CSV.

## 3. Flujo detallado

### 3.1 `main()`

```cpp
srand(time(0));
int contadorID = 1;
do {
  cin >> opcion;
  if (opcion == 1) jugarPartida(contadorID);
  else if (opcion == 2) leerHistorialDisco();
} while (opcion != 3);
```

### 3.2 `jugarPartida(int& contadorID)`

1. `p.idPartida = contadorID++`.
2. `cin.ignore(); getline(cin, p.jugador);` — ver §5.
3. `cin >> opcJugador` → mapea 1/2/3 a Piedra/Papel/Tijera
   (cualquier otro valor cae en Tijera por `else`; mejora posible: validar).
4. IA: `(rand() % 3) + 1` → 1..3.
5. Reglas:
   - iguales → Empate;
   - Piedra>Tijera, Papel>Piedra, Tijera>Papel → Victoria;
   - resto → Derrota.
6. Llama a `guardarEnDisco(p)`.

### 3.3 `guardarEnDisco(const Partida& p)` — escritura

```cpp
ofstream archivo("src/historial_partidas.txt", ios::app);
// ...
archivo << p.idPartida << "," << p.jugador << ","
        << p.eleccionJugador << "," << p.eleccionIA << ","
        << p.resultado << endl;
archivo.close();
```

- Ruta relativa a la raíz del proyecto (el `.exe` se lanza desde la raíz).
- `ios::app` (append): agrega al final sin truncar. Sin `ios::app`,
  `ofstream` abre en `ios::out` y **borra** el contenido previo.
- Verifica `is_open()` y reporta por `cerr` si falla.
- Formato CSV simple, sin comillas ni escape (restricción conocida:
  no usar comas en el nickname).

### 3.4 `leerHistorialDisco()` — lectura

```cpp
ifstream archivo("src/historial_partidas.txt");
while (getline(archivo, idStr, ',') &&
       getline(archivo, jugador, ',') &&
       getline(archivo, elJug, ',') &&
       getline(archivo, elIA, ',') &&
       getline(archivo, resultado)) { /* mostrar */ }
```

- Si no abre → aún no hay partidas (primera ejecución).
- Lee campo por campo delimitado por `,`; el último con delimitador
  `\n` por defecto. Cuenta `total` y muestra el resumen.
- Maneja archivo vacío (`total == 0`).

## 4. Librerías

- `<iostream>`: `cout`, `cin`, `cerr`, `getline(cin, ...)`.
- `<fstream>`: `ofstream` (salida), `ifstream` (entrada).
- `<string>`: `std::string`, comparación con `==`.
- `<cstdlib>`: `rand()`, `srand()`.
- `<ctime>`: `time(0)` como semilla.

## 5. Punto crítico: `cin.ignore()` y el búfer

Secuencia `cin >> opcion` deja el `\n` (Enter) en el búfer.
Sin limpieza, el siguiente `getline()` leería esa línea vacía
y "saltearía" el nombre. `cin.ignore()` descarta ese carácter
pendiente antes de `getline(cin, p.jugador)`.

## 6. Compilación, ejecución y pruebas

```powershell
g++ -std=c++11 src/main.cpp -o src/piedrapapelotijera.exe
.\src\piedrapapelotijera.exe
```

Pruebas sugeridas:

1. Compilación limpia sin warnings con `-std=c++11`.
2. Jugar 3 partidas con nombres con espacios → verificar 3 líneas nuevas en el `.txt`.
3. Cerrar consola, reabrir, opción 2 → el historial persiste.
4. Borrar/renombrar el `.txt` → opción 2 debe mostrar el aviso, no colgarse.
5. Probar opción inválida (`9`, letra) → mensaje de error y el menú continúa.

## 7. Limitaciones y mejoras futuras

- `contadorID` reinicia en 1 en cada ejecución (no lee el máximo del archivo).
  Mejora: al iniciar, contar líneas del `.txt` para continuar la numeración.
- Sin validación de `opcJugador` ni de `cin` fallido (si se ingresa texto
  donde se espera número, `cin` entra en fallo). Mejora: validar rango y
  limpiar `cin` con `cin.clear()` + `ignore()`.
- CSV sin escape: documentado en el manual de usuario.
- Sin fecha/hora: se podría agregar `time()` formateado como sexto campo.
- Adaptación al P.I.A.: reutilizar `guardarEnDisco`/`leerHistorialDisco`
  para logs de sensores, usuarios, stock o fichajes (ver informe §5).

## 8. Mantenimiento

- No cambiar la ruta `"src/historial_partidas.txt"` sin actualizar ambas
  funciones y los manuales.
- Mantener `.gitignore` con `*.exe` para no versionar binarios.
- Versionado: cualquier cambio de formato CSV implica subir versión
  (v1.1.0) y registrar en `docs/CHANGELOG.md`.

## 9. Datos del estudiante (completar)

- Nombre y Apellido: Teo Laguna
- Curso: 5° 3° Grupo: A / B
- Fecha: 16/10/2026

---
*Manual del programador v1.0.0 — Actividad 7 LPR 2026.*
