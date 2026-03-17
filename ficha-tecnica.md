# Ficha Técnica: Git - branch, merge y resolución de conflictos

**Curso:** Fundamentos de Ingeniería de Software

**Integrantes:** Joaquín Rodríguez, Tiago Irrazábal, Juan Rafael Menéndez

---

## 1. Fuentes de Información

- Chacon, S. & Straub, B. (2014). *Pro Git* (2nd ed.): https://git-scm.com/book/en/v2
- Documentación oficial de Git: https://git-scm.com/docs
- GitHub Docs – Understanding branches: https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-branches
- ¿Qué es Git? - Microsoft Build: https://learn.microsoft.com/es-es/devops/develop/git/what-is-git

---

## 2. Definiciones

**Git** es un sistema de control de versiones distribuido, lo que significa que un clon local del proyecto es un repositorio de control de versiones completo. Estos repositorios locales totalmente funcionales facilitan el trabajo sin conexión o de forma remota. Los desarrolladores confirman su trabajo localmente y, a continuación, sincronizan su copia del repositorio con la copia en el servidor. Este paradigma difiere del control de versiones centralizado en el que los clientes deben sincronizar el código con un servidor antes de crear nuevas versiones de código.

**Rama (Branch):** En Git, cada desarrollador guarda sus cambios en su propio repositorio local, lo que puede generar múltiples líneas de desarrollo paralelas partiendo de un mismo commit. Para manejar esta separación, Git utiliza las ramas: punteros ligeros que apuntan a trabajos en curso. Esto permite aislar cambios sin afectar el código principal. Una vez finalizado el trabajo en una rama, este puede fusionarse nuevamente en la rama principal del equipo.

**HEAD:** Es una referencia especial que indica la rama (y por ende el commit) sobre la cual se está trabajando actualmente.

**Merge (Fusión):** Es la operación que integra los cambios de una rama en otra. Git soporta dos estrategias principales:

**Fast-forward:** cuando la rama principal no tuvo cambios desde que se creó la rama secundaria, Git simplemente mueve el puntero hacia adelante.

**Conflicto:** Ocurre cuando dos ramas modifican la misma línea de un archivo. Git no puede resolverlo automáticamente y requiere intervención manual del desarrollador.

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

# 6. Volver a la rama principal y fusionar
git switch main
git merge feature/login

# 7. Eliminar la rama ya integrada
git branch -d feature/login
```

En caso de conflicto durante el merge, Git marcará los archivos afectados. Se deben editar manualmente, luego ejecutar `git add` sobre los archivos resueltos y finalizar con `git commit`.

---

## 4. Recursos de Aprendizaje

| Recurso | Tipo | Enlace |
|---|---|---|
| Pro Git – Scott Chacon & Ben Straub | Libro (gratuito) | https://git-scm.com/book/en/v2 |
| Documentación oficial de Git | Referencia técnica | https://git-scm.com/docs |
| Learn Git Branching | Simulador visual | https://learngitbranching.js.org |

