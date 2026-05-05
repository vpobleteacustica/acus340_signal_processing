# SETUP - ACUS340 Signal Processing

## Cómo actualizar el repositorio del curso

Durante el curso, el repositorio puede ser actualizado con nuevos notebooks, actividades o archivos de apoyo.

Si usted ya clonó el repositorio en su computador, **no es necesario borrarlo ni clonarlo nuevamente**.  
Lo correcto es actualizar su copia local usando `git pull`.

---

## Paso 1: entrar a la carpeta del repositorio

Desde la terminal, ubíquese dentro de la carpeta del proyecto:

```bash
cd ruta/al/repositorio/acus340_signal_processing
```

Por ejemplo:

```bash
cd ~/Documents/acus340_signal_processing
```

---

## Paso 2: revisar el estado del repositorio

Antes de actualizar, revise si tiene cambios locales:

```bash
git status
```

---

## Caso A: no tiene cambios locales

Si aparece un mensaje similar a:

```text
nothing to commit, working tree clean
```

puede actualizar directamente con:

```bash
git pull origin main
```

Esto descargará los nuevos notebooks, actividades o archivos agregados por el profesor.

---

## Caso B: tiene cambios locales

Si `git status` muestra archivos modificados, **no borre el repositorio y no clone nuevamente**.

Primero guarde sus cambios locales con un commit:

```bash
git add .
git commit -m "Save my local work"
```

Luego actualice el repositorio:

```bash
git pull origin main
```

De esta manera, conserva su trabajo y recibe las actualizaciones del curso.

---

## Alternativa: guardar cambios temporalmente con stash

Si todavía no quiere hacer un commit, puede guardar temporalmente sus cambios con:

```bash
git stash
git pull origin main
git stash pop
```

Sin embargo, para este curso se recomienda usar la opción con `git add`, `git commit` y luego `git pull`, porque deja un registro claro del trabajo realizado.

---

## Resumen rápido

Si no tiene cambios locales:

```bash
git status
git pull origin main
```

Si tiene cambios locales:

```bash
git status
git add .
git commit -m "Save my local work"
git pull origin main
```

---

## Importante

No borre su carpeta local del repositorio, ya que podría perder el trabajo que ha realizado.

La forma recomendada de actualizar el repositorio del curso es:

1. Revisar el estado con `git status`.
2. Guardar los cambios locales si existen.
3. Actualizar con `git pull origin main`.
