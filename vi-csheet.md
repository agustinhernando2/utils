# Guía básica de vi para principiantes

El editor **vi** es un editor de texto muy utilizado en sistemas Unix/Linux. Funciona en **modo comando** y **modo de inserción**, lo que permite editar archivos de manera eficiente sin necesidad de un entorno gráfico.

## 1. Abrir y salir de vi
- `vi archivo.txt` → Abre el archivo `archivo.txt`
- `:w` → Guarda los cambios
- `:q` → Sale del editor
- `:wq` o `ZZ` → Guarda y sale
- `:q!` → Sale sin guardar

## 2. Modo comando vs. modo inserción
- **Modo comando**: Es el modo predeterminado al abrir **vi**. Permite navegar y ejecutar comandos.
- **Modo inserción**: Permite escribir texto en el archivo. Se activa con:
  - `i` → Inserta antes del cursor
  - `a` → Inserta después del cursor
  - `o` → Nueva línea debajo
  - `O` → Nueva línea arriba
- **Para salir del modo inserción**, presiona `Esc`.

## 3. Movimientos del cursor
- `h` → Izquierda
- `l` → Derecha
- `j` → Abajo
- `k` → Arriba
- `w` → Avanza una palabra
- `b` → Retrocede una palabra
- `^` → Inicio de línea
- `$` → Fin de línea
- `G` → Ir a la última línea
- `nG` o `:n` → Ir a la línea `n`

## 4. Edición de texto
- `x` → Borra un carácter
- `dd` → Borra una línea
- `dw` → Borra una palabra
- `d$` → Borra hasta el final de la línea
- `u` → Deshacer la última acción (**Ctrl+Z en otros editores**)
- `<ctrl>r` → Rehacer la última acción
- `yy` → Copiar una línea
- `p` → Pegar después del cursor
- `P` → Pegar antes del cursor

## 5. Buscar texto
- `/texto` → Busca "texto" hacia adelante
- `?texto` → Busca "texto" hacia atrás
- `n` → Repite la última búsqueda en la misma dirección
- `N` → Repite la última búsqueda en la dirección opuesta

## 6. Buscar y reemplazar
```vim
:%s/viejo/nuevo/g
