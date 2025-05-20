
---

## 🚀 Cheatsheet de GitHub (Conciso)

### ⚙️ Lo Básico

* **`git init`**: Inicializa un nuevo repositorio Git local.
* **`git clone [URL]`**: Clona un repositorio remoto a tu máquina local.
* **`git add .`**: Prepara todos los cambios para el próximo commit.
* **`git commit -m "Tu mensaje"`**: Guarda los cambios preparados en tu historial local.
* **`git push origin [rama]`**: Envía tus commits locales al repositorio remoto.
* **`git pull origin [rama]`**: Descarga y aplica los cambios del repositorio remoto a tu rama local.
* **`git status`**: Muestra el estado del área de trabajo y del staging.
* **`git log`**: Muestra el historial de commits.

### 🌳 Ramas

* **`git branch`**: Lista las ramas locales.
* **`git branch [nombre_rama]`**: Crea una nueva rama local.
* **`git checkout [nombre_rama]`**: Cambia a la rama especificada.
* **`git merge [nombre_rama]`**: Fusiona los cambios de la rama especificada a la rama actual.
* **`git branch -d [nombre_rama]`**: Elimina una rama local (solo si está fusionada).

### 💥 Resolución de Conflictos

* **`git diff`**: Muestra las diferencias entre archivos o entre el área de trabajo y el staging.
* Cuando un `pull` o `merge` resulta en conflictos, Git los marca. Debes **editar manualmente** los archivos para resolver las secciones conflictivas (`<<<<<<<`, `=======`, `>>>>>>>`).
* Después de resolver, **`git add [archivo_con_conflicto]`** y **`git commit -m "Mensaje de resolución"`**.

---

## 📦 Trabajar con Múltiples Repositorios (Submódulos)

Los **submódulos Git** permiten incrustar un repositorio Git dentro de otro como un subdirectorio. Esto es útil para gestionar dependencias de proyectos.

* **`git submodule add [URL_repositorio] [ruta_local]`**: Agrega un repositorio como submódulo en la ruta especificada.
* **`git submodule update --init --recursive`**: Inicializa, clona y actualiza los contenidos de los submódulos después de clonar el repositorio principal o si hay cambios en los submódulos.

---

## 🌐 Trabajando con Remotos (GitHub)

* `git remote -v`: Muestra los remotos configurados.
* `git remote add origin <url>`: Agrega un remoto llamado 'origin' (comúnmente la URL de tu repo GitHub).
* `git push -u origin <nombre-rama>`: Sube los commits locales a la rama remota y configura el seguimiento.
* `git push`: Sube los cambios a la rama remota configurada (después de la primera vez).
* `git pull`: Descarga y fusiona los cambios del repositorio remoto a tu rama local.
* `git fetch`: Descarga los cambios del repositorio remoto pero no los fusiona.

---

## ↩️ Deshaciendo Cambios

* `git reset --hard HEAD`: Descarta todos los cambios no commiteados y regresa al último commit. **¡Cuidado, es destructivo!**
* `git reset <archivo>`: Quita un archivo del área de staging (pero mantiene los cambios).
* `git revert <commit-hash>`: Crea un nuevo commit que deshace los cambios de un commit anterior. No reescribe el historial.

---

## 🔄 GitFlow (Flujo de Trabajo Simplificado)

GitFlow es una estrategia de ramificación que organiza el desarrollo y el lanzamiento de versiones de software.

* **`master` (o `main`)**:
    * Contiene el código **estable y listo para producción**. Los cambios solo llegan aquí mediante merges de `release` o `hotfix`.
* **`develop`**:
    * Rama de **integración principal** para nuevas funcionalidades. Todo el nuevo desarrollo se realiza a partir de aquí.
* **`feature/[nombre_feature]`**:
    * Ramas creadas a partir de `develop` para desarrollar **nuevas funcionalidades** de forma aislada. Una vez completadas, se fusionan de nuevo en `develop`.
* **`release/[version]`**:
    * Ramas creadas a partir de `develop` para **preparar un nuevo lanzamiento**. Aquí se hacen pruebas finales y correcciones de errores específicas de la versión. Se fusionan en `master` y `develop`.
* **`hotfix/[nombre_hotfix]`**:
    * Ramas creadas directamente desde `master` para **solucionar errores críticos en producción**. Una vez resueltos, se fusionan en `master` y `develop`.

---

### ⚡ Atajos y Utilidades Avanzadas

* **`git commit -am "Mensaje"`**: Combina `git add .` y `git commit -m`. Útil para cambios en archivos ya seguidos.
* **`git reset --hard HEAD`**: Descarta todos los cambios locales no commiteados y restaura el estado del último commit. **¡Usar con precaución!**
* **`git reflog`**: Muestra un registro de todas las operaciones HEAD, lo que puede ayudar a recuperar commits "perdidos".
* **`git stash`**: Guarda temporalmente los cambios en el área de trabajo y el staging sin commitear.
    * **`git stash save "mensaje"`**: Guarda los cambios con un mensaje.
    * **`git stash list`**: Muestra los stashes guardados.
    * **`git stash pop`**: Aplica el stash más reciente y lo elimina de la lista.
    * **`git stash apply`**: Aplica el stash más reciente pero lo mantiene en la lista.

## Basic aliases
```bash
# Log simplificado con ramas y colores
git config --global alias.lg "log --oneline --graph --all --decorate"

# Status corto y claro
git config --global alias.st "status -sb"

# Añadir todos los cambios
git config --global alias.a "add ."

# Descartar cambios locales (con cuidado)
git config --global alias.undo "checkout --"

# Commit rápido
git config --global alias.c "commit"

# Commit firmado (como tu alias `cis`)
git config --global alias.cis "commit -S"
```
---

### **Historial y comparación**
```bash
# Ver el último commit
git config --global alias.last "log -1 HEAD"

# Ver diferencias de manera colorida
git config --global alias.d "diff --color"

# Ver qué archivo ha cambiado (con nombres)
git config --global alias.sdiff "diff --stat"

# Mostrar el autor de cada línea (blame simplificado)
git config --global alias.bl "blame"

---

#### **Rebase y merges**
```bash
# Rebase interactivo simplificado
git config --global alias.rbi "rebase -i"

# Continuar rebase
git config --global alias.rbc "rebase --continue"

# Abortar rebase
git config --global alias.rba "rebase --abort"

#### **Ramas**
# Crear y cambiar a una rama nueva
git config --global alias.new "checkout -b"

# Listar ramas ordenadas
git config --global alias.br "branch -vv"

# Eliminar rama remota
git config --global alias.delr "push origin --delete"

---

#### **Trabajando con remotos**
```bash
# Mostrar remotos
git config --global alias.remote "remote -v"

# Actualizar remoto y ramas locales
git config --global alias.up "pull --rebase --prune"

# Subir cambios rápidamente
git config --global alias.psh "push"

# Configurar un alias global para un push forzado seguro
git config --global alias.fpush "push --force-with-lease"

## ADD 

nano ~/.gitconfig

[alias]
        c = commit
        amend = commit --amend
        cis = commit -S
        list-aliases = config --get-regexp ^alias\\.
        lg = log --oneline --graph --all --decorate
        st = status -sb
        a = add .
        undo = checkout --
        last = log -1 HEAD
        d = diff --color
        rbi = rebase -i
        new = checkout -b
        br = branch -vv
        psh = push
        fpush = push --force-with-lease
	ch = checkout


# check changes
git config --global --get-regexp alias
