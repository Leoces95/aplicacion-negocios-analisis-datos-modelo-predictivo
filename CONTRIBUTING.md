# Cómo contribuir (flujo de Pull Requests)

## Reglas del equipo
1. **`main` siempre funciona.** Nadie hace push directo a `main`; todo entra por Pull Request (PR).
2. **Un PR = una tarea.** Ramas con prefijo: `feat/` (funcionalidad), `fix/` (corrección), `docs/` (documentación).
3. **Mínimo 1 aprobación** de otro integrante antes de hacer merge. Quien revisa **ejecuta** el código, no solo lo lee.
4. **Cada quien edita solo su notebook.** Si necesitas algo en el notebook de otro, coméntalo en su PR o abre un *issue*.
5. **No se suben datos** (`data/` está en `.gitignore`). Los datos se regeneran con `python -m src.etl`.
6. Antes de hacer commit de un notebook: **Kernel → Restart & Run All**, para que las salidas sean reproducibles y estén en orden.

## Paso a paso (para cualquier integrante)

```bash
# 0. Una sola vez: clonar el repo y configurar tu identidad
git clone https://github.com/Leoces95/aplicacion-negocios-analisis-datos-modelo-predictivo.git
cd aplicacion-negocios-analisis-datos-modelo-predictivo
git config user.name "Tu Nombre"
git config user.email "tu-correo-de-github@ejemplo.com"

# 1. Partir SIEMPRE de main actualizado
git checkout main
git pull origin main

# 2. Crear tu rama
git checkout -b feat/mi-tarea

# 3. Trabajar... y guardar cambios
git add src/archivo.py notebooks/mi_notebook.ipynb
git commit -m "feat(etl): describe en presente qué hace el cambio"

# 4. Subir la rama
git push -u origin feat/mi-tarea
```

5. En GitHub aparece el botón **"Compare & pull request"**. Llena la plantilla, asigna un **revisor** y crea el PR.
6. Si el revisor pide cambios: corriges en la **misma rama**, haces commit y push, y el PR se actualiza solo.
7. Cuando esté aprobado, el autor hace **"Squash and merge"** y borra la rama.
8. Todos los demás hacen `git checkout main` y luego `git pull` para traer los cambios.

## Si tu rama quedó desactualizada (alguien hizo merge antes que tú)
```bash
git checkout main
git pull origin main
git checkout feat/mi-tarea
git merge main          # resuelve conflictos si aparecen, luego commit
git push
```

## Convención de mensajes de commit
`tipo(área): descripción corta`, donde tipo es `feat`, `fix`, `docs`, `refactor` o `chore`.
Ejemplos: `feat(eda): análisis de retrasos por región`, `fix(etl): corrige imputación de peso`.

## Configuración recomendada del repo (la hace Leonel como dueño)
GitHub → **Settings → Branches → Add branch protection rule** para `main`:
- ✅ Require a pull request before merging → Require approvals: **1**
- ✅ Do not allow bypassing the above settings

Además: **Settings → Collaborators → Add people**, para agregar a Harol, Yulieth y Jalvi con permiso de escritura.
