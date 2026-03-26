# Ficha Técnica: Git – Branch, Merge y Resolución de Conflictos

**Curso:** Fundamentos de Ingeniería de Software
**Integrantes:** Joaquín Rodríguez, Tiago Irrazábal, Juan Rafael Menéndez

---

## 1. Fuentes de Información

- Chacon, S. & Straub, B. (2014). *Pro Git* (2nd ed.): https://git-scm.com/book/en/v2
- Documentación oficial de Git: https://git-scm.com/docs
- GitHub Docs – Understanding branches: https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-branches
- ¿Qué es Git? – Microsoft Learn: https://learn.microsoft.com/es-es/devops/develop/git/what-is-git
- Git MERGE vs REBASE: Everything You Need to Know – ByteByteGo (YouTube): https://www.youtube.com/watch?v=0chZFIZLR_0

---

## 2. Definiciones

**Git** es un sistema de control de versiones distribuido, lo que significa que un clon local del proyecto es un repositorio de control de versiones completo. Estos repositorios locales facilitan el trabajo sin conexión o de forma remota. Los desarrolladores confirman su trabajo localmente y, a continuación, sincronizan su copia del repositorio con la copia en el servidor.

**Modelo de snapshots:** A diferencia de otros sistemas de control de versiones que registran los cambios como diferencias entre archivos, Git almacena la información como una serie de snapshots del proyecto completo. Cada vez que se realiza un commit, Git guarda una referencia a ese snapshot. Si un archivo no cambió, Git no lo vuelve a guardar sino que enlaza al archivo idéntico ya almacenado. Esto hace que las operaciones de Git sean muy rápidas, ya que casi todo se ejecuta de forma local sin necesidad de consultar un servidor.

**Rama (Branch):** En Git, cada desarrollador guarda sus cambios en su propio repositorio local, lo que puede generar múltiples líneas de desarrollo paralelas partiendo de un mismo commit. Para manejar esta separación, Git utiliza las ramas: punteros ligeros que apuntan a trabajos en curso. Esto permite aislar cambios sin afectar el código principal. Una vez finalizado el trabajo en una rama, este puede fusionarse nuevamente en la rama principal del equipo.

**HEAD:** Es una referencia especial que indica la rama y el commit sobre el cual se está trabajando actualmente.

**Merge (Fusión):** Es el proceso de integrar los cambios de una rama en otra mediante el comando `git merge`. Git aplica distintas estrategias según cómo haya evolucionado el historial:

- **Fast-forward:** Ocurre cuando el commit de la rama a fusionar es un ancestro directo de la rama destino, es decir, no hay trabajo divergente. En ese caso, Git simplemente mueve el puntero hacia adelante hasta alcanzar el commit más reciente, sin crear un nuevo commit de fusión.

- **Merge a tres bandas (Three-way merge):** Cuando el historial ha divergido, Git realiza una fusión utilizando tres referencias: las puntas de las dos ramas y su ancestro común más reciente. El resultado es un nuevo *commit de fusión* especial que tiene más de un padre.

**Conflicto de fusión:** Ocurre cuando dos ramas modifican la misma parte de un mismo archivo de forma distinta. Git no puede fusionarlas automáticamente y pausa el proceso. Git añade marcadores de conflicto al archivo afectado: la sección entre `<<<<<<<` y `=======` corresponde a la rama actual (HEAD), y la sección entre `=======` y `>>>>>>>` corresponde a la rama entrante. Para resolver el conflicto se debe editar el archivo eligiendo una versión o combinando ambas, eliminar los marcadores, y luego ejecutar `git add` para marcar el archivo como resuelto y `git commit` para finalizar la fusión.

**Rebase:** Es una forma alternativa de integrar cambios entre ramas. En lugar de crear un commit de fusión, toma los commits de una rama y los reaplica uno a uno sobre otra rama. El resultado es un historial lineal, como si todo el trabajo hubiera ocurrido en serie. La diferencia clave respecto al merge es que el rebase reescribe el historial, mientras que el merge lo preserva.

**Squash:** Es una técnica que combina todos los commits de una rama en un único commit antes de integrarlos. Produce el mismo estado en el repositorio que un merge real, pero sin crear un commit de fusión. El commit resultante tiene un solo padre. Se utiliza para mantener un historial más limpio y ordenado.

**Reset:** Permite deshacer commits moviendo el puntero de la rama hacia atrás en el historial. En su forma `--soft`, deshace el commit pero conserva los cambios en el área de staging, lo que permite rehacerlo con modificaciones. Al reescribir el historial, solo debe usarse sobre commits que aún no fueron compartidos con el equipo.

**Revert:** Es la forma segura de deshacer un commit que ya fue compartido. En lugar de reescribir el historial, crea un nuevo commit que aplica los cambios inversos al commit original. El historial se preserva intacto, lo que lo hace adecuado para trabajo en equipo.

**Tag:** Es una referencia fija a un commit específico, utilizada para marcar hitos importantes del proyecto como versiones o releases. A diferencia de las ramas, los tags no avanzan con nuevos commits. Git soporta tags simples (solo un nombre) y tags anotados (con mensaje y metadatos).

---

## 3. Demostración Práctica

A continuación se muestra un flujo típico de trabajo con ramas en Git:

```bash
# 1. Inicializar un repositorio
git init mi-proyecto
cd mi-proyecto

# 2. Crear un archivo y hacer el primer commit
echo "# Mi Proyecto" > README.md
git add README.md
git commit -m "commit inicial"

# 3. Crear una nueva rama para una funcionalidad
git branch feature/login

# 4. Moverse a la nueva rama
git switch feature/login

# 5. Realizar cambios y confirmarlos
echo "función login implementada" >> README.md
git add README.md
git commit -m "agrega funcionalidad de login"

# 6. Volver a la rama principal y fusionar (fast-forward)
git switch main
git merge feature/login

# 7. Eliminar la rama ya integrada
git branch -d feature/login
```

---

## 4. Recursos de Aprendizaje

| Recurso | Tipo | Enlace |
|---|---|---|
| *Pro Git* – Scott Chacon & Ben Straub | Libro (gratuito) | https://git-scm.com/book/en/v2 |
| Documentación oficial de Git | Referencia técnica | https://git-scm.com/docs |
| Learn Git Branching | Simulador visual | https://learngitbranching.js.org |

---
