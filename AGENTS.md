# Contexto del proyecto

Este repositorio es una implementación en C de ORCA, un entorno de livecoding
en terminal. El código principal del editor está en `tui_main.c`; la simulación
de operadores está en `sim.c`.

## Trabajo reciente

- Trabajar directamente en `master`. No crear una rama nueva a menos que el
  usuario pida explícitamente crearla.
- Se agregó entrada MIDI con el operador `&`, que alterna el contenido de la
  celda inferior entre `*` y `.` al recibir note-on coincidentes. La
  documentación y un ejemplo están en `README.md` y
  `examples/setups/midi-toggle.orca`.
- Se agregó el atajo `Ctrl+/` para alternar comentario sobre una selección
  rectangular. Orca usa `#` para comentar hasta el siguiente `#` en la misma
  fila. El atajo escribe los marcadores en las celdas vacías inmediatamente a
  izquierda y derecha de cada fila seleccionada, sin desplazar ni reemplazar
  contenido. Si todos los pares de bordes ya contienen `#`, los quita. La
  operación no hace cambios si los bordes no están disponibles o no forman un
  estado consistente. En terminales que codifican `Ctrl+/` como ASCII Unit
  Separator, la entrada se reconoce como `CTRL_PLUS('_')`.
- El atajo aparece en la ayuda de controles que se abre con `?` y en el menú
  principal.

## Compilación

Usar `make release` para compilar el ejecutable en `build/orca`. `make debug`
genera la versión de depuración.

## Cuidado al modificar

- Mantener intacto el contenido del proyecto al comentar selecciones; sólo se
  escriben o quitan los marcadores `#` de las celdas de borde.
- El ancho de la grilla es compartido por todas las filas. No insertar columnas
  ni desplazar contenido para comentar.
- La función de comentario y el despacho de teclas viven en `tui_main.c`; la
  lista visible de atajos se mantiene en `push_controls_msg`.
