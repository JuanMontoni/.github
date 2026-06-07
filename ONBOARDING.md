# 📋 Onboarding — Laboratorio de Sistemas Embebidos (UTN-FRA)

Bienvenido/a al LSE. Este documento es de lectura **obligatoria** antes de comenzar a trabajar en cualquier repositorio de la organización [`utn-fra-lse`](https://github.com/utn-fra-lse).

> **Tu primera tarea está al final de este documento.**

---

## Índice

1. [Roles](#1-roles)
2. [Convenciones de commits](#2-convenciones-de-commits)
3. [Convenciones de ramas](#3-convenciones-de-ramas)
4. [Issues: cómo crearlos y gestionarlos](#4-issues-cómo-crearlos-y-gestionarlos)
5. [Pull Requests: cómo crearlos y gestionarlos](#5-pull-requests-cómo-crearlos-y-gestionarlos)
6. [Uso de GitHub Projects (Kanban)](#6-uso-de-github-projects-kanban)
7. [Tarea de onboarding obligatoria](#7-tarea-de-onboarding-obligatoria)

---

## 1. Roles

La organización maneja tres roles principales. Cada uno tiene permisos distintos en los repositorios.

| Rol | Descripción | Permisos |
|-----|-------------|----------|
| **Docente** | Responsable técnico o académico de uno o más proyectos. Aprueba PRs y coordina el trabajo del equipo. | Write + Review en todos los repos |
| **Becario** | Integrante activo con contraprestación económica. Trabaja en issues asignados. | Write en repos del proyecto asignado |
| **Colaborador externo** | Participación puntual o temporal. Sin acceso a datos sensibles. | Read o Write limitado por repo |

Los teams de la organización son:
- `@utn-fra-lse/docentes`
- `@utn-fra-lse/becarios`
- `@utn-fra-lse/externos`

---

## 2. Convenciones de commits

Usamos **Conventional Commits**. El formato es:

```
<tipo>(<scope opcional>): <descripción corta en imperativo>

[cuerpo opcional]

[footer opcional: refs #issue, breaking changes]
```

### Tipos válidos

| Tipo | Cuándo usarlo |
|------|---------------|
| `feat` | Nueva funcionalidad |
| `fix` | Corrección de bug |
| `docs` | Solo documentación |
| `style` | Formato, espacios, sin cambio de lógica |
| `refactor` | Refactorización sin feat ni fix |
| `test` | Agregar o corregir tests |
| `chore` | Tareas de build, CI, dependencias |
| `perf` | Mejora de performance |

### Ejemplos

```
feat(uart): agregar soporte para baudrate 115200
fix(adc): corregir overflow en lectura de canal 3
docs(readme): actualizar instrucciones de compilación
chore(ci): agregar workflow de lint
```

### Reglas

- La descripción va en **español**, en **imperativo** y en **minúsculas**
- Sin punto final en el subject
- Máximo 72 caracteres en el subject
- Referenciar el issue relacionado en el footer: `Refs #12` o `Closes #12`

---

## 3. Convenciones de ramas

### Nomenclatura

```
<tipo>/<issue-número>-<descripcion-corta>
```

| Tipo | Uso |
|------|-----|
| `feat/` | Nueva funcionalidad |
| `fix/` | Corrección de bug |
| `docs/` | Cambios de documentación |
| `refactor/` | Refactorización |
| `chore/` | Mantenimiento, CI, dependencias |

### Ejemplos

```
feat/42-driver-spi
fix/17-timeout-i2c
docs/8-agregar-diagrama-hardware
```

### Ramas protegidas

| Rama | Descripción | Protección |
|------|-------------|------------|
| `main` | Código estable, revisado y aprobado | PR obligatorio + 1 aprobación de `@docentes` |
| `develop` | Integración continua antes de pasar a main | PR obligatorio |

**No se hace push directo a `main` ni a `develop`.**

---

## 4. Issues: cómo crearlos y gestionarlos

### Cuándo crear un issue

Cada unidad de trabajo debe tener un issue. Esto incluye:
- Una nueva funcionalidad o tarea técnica
- Un bug encontrado
- Una tarea de documentación
- Una actividad del laboratorio (ensayo, medición, reunión de revisión)

### Cómo crear un issue

1. Ir al repositorio correspondiente → pestaña **Issues** → **New Issue**
2. Elegir el template adecuado (bug, feature, tarea, actividad)
3. Completar **todos** los campos del template
4. Asignar:
   - **Assignees**: quién lo trabaja
   - **Labels**: tipo y prioridad
   - **Project**: tablero correspondiente (ver sección 6)
   - **Milestone**: entrega o fecha límite asociada (si aplica)

### Labels estándar

Los labels clasifican el área temática y el estado de un issue. Se pueden combinar: un issue puede tener `firmware` + `bug`, o `hardware` + `bloqueado` al mismo tiempo.

**Área temática** — describe de qué trata el issue:

| Label | Descripción |
|-------|-------------|
| `administración` | Tareas que involucren relevamientos, organización o cualquiera similar |
| `documentación` | Tareas relacionadas a confección de artículos, documentos, apuntes o presentaciones |
| `firmware` | Tareas relacionadas a software embebido |
| `fpga` | Tareas relacionadas a FPGA |
| `hardware` | Tareas de diseño, ensayo o fabricación de circuitos |
| `investigación` | Tareas relacionadas a capacitaciones e investigación sobre alguna temática |
| `testing` | Ensayos, validación y verificación de desarrollos existentes |
| `drivers` | Desarrollo o mantenimiento de drivers y HALs de periféricos |
| `rtos` | Tareas relacionadas a sistemas operativos de tiempo real |
| `pcb` | Diseño de circuito impreso, revisión de layout o fabricación |

**Estado / condición** — se agregan sobre el label temático cuando aplica:

| Label | Descripción |
|-------|-------------|
| `bug` | Comportamiento incorrecto o inesperado en cualquier área |
| `bloqueado` | Issue que no puede avanzar por una dependencia externa |

### Ciclo de vida de un issue

```
Backlog → Todo → En proceso → En revisión → Terminado
```

Cuando empezás a trabajar en un issue, movelo a **En proceso** en el tablero y creá la rama correspondiente.

---

## 5. Pull Requests: cómo crearlos y gestionarlos

### Cuándo abrir un PR

Cuando una rama está lista para revisión. No esperes a tener todo perfecto: podés abrir un **Draft PR** mientras trabajás para visibilidad del equipo. Un Draft PR es preferible a usar `[WIP]` en el título — GitHub lo indica visualmente y bloquea el merge accidental.

### Título del PR

Usamos el mismo estilo que los commits: **Conventional Commits**. Esto permite que la lista de PRs sea escaneable con la misma lógica que el historial, sin agregar una convención nueva.

```
<tipo>(<scope opcional>): <descripción corta>
```

Ejemplos:

```
feat(spi): agregar driver para sensor MPU6050
fix(uart): corregir pérdida de datos en interrupción RX
docs(readme): agregar diagrama de conexión
chore(ci): actualizar versión de arm-none-eabi-gcc
```

### Cómo crear un PR

1. Desde la rama de trabajo → **Compare & pull request**
2. Completar el template (se carga automáticamente)
3. Asignar:
   - **Reviewers**: al menos un docente del team `@utn-fra-lse/docentes`
   - **Assignees**: quien abre el PR
   - **Labels**: mismos que el issue relacionado
   - **Project**: mismo tablero que el issue
   - **Linked issue**: usar `Closes #NNN` en la descripción para cierre automático

### Reglas de revisión

- **Nadie mergea su propio PR**
- Al menos **1 aprobación** para mergear a `develop`
- Al menos **1 aprobación** de un docente para mergear a `main`
- Los comentarios de revisión deben resolverse antes de mergear

### Tipos de feedback en revisión

- ✅ **Approve**: listo para mergear
- 💬 **Comment**: observación sin bloqueo
- ❌ **Request changes**: requiere correcciones antes de aprobar

---

## 6. Uso de GitHub Projects (Kanban)

### Estructura de tableros

La organización tiene dos tipos de tableros:

| Tablero | Alcance | Administrador |
|---------|---------|---------------|
| **Actividades Generales del Lab** | Tareas operativas, administrativas y transversales | Docentes |
| **[Nombre Proyecto]** | Issues y PRs del proyecto específico | Docente responsable del proyecto |

### Columnas Kanban

Todos los tableros usan las mismas columnas:

```
📥 Backlog  →  📋 Todo  →  🚧 Bloqueado  →  🔧 En proceso  →  👀 En revisión  →  ✅ Terminado
```

| Columna | Significado |
|---------|-------------|
| **Backlog** | Ideas y tareas no planificadas aún |
| **Todo** | Tareas listas para arrancar |
| **Bloqueado** | Tareas con las que no se puede avanzar por una dependencia externa |
| **En proceso** | En trabajo activo (máx. 2 por persona) |
| **En revisión** | PR abierto, esperando revisión |
| **Terminado** | Completadas y mergeadas |

Un item en **Bloqueado** debe tener un comentario explicando qué lo bloquea y, si aplica, una referencia al issue del que depende.

### Campos personalizados de cada item

Los campos que usamos en el tablero son:

| Campo | Tipo | Uso |
|-------|------|-----|
| `Priority` | Select | `Urgent / High / Medium / Low` — prioridad del item |
| `Start date` | Fecha | Fecha en que se empieza a trabajar en el item |
| `Target date` | Fecha | Fecha límite o de entrega esperada |

Las fechas son especialmente importantes: son las que alimentan la vista **Roadmap** del tablero, que permite ver la distribución temporal de los items en curso y planificados. Un item sin fechas no aparece en el roadmap. Completarlas es obligatorio para cualquier item en **Todo** o superior.

### Reglas del tablero

- **No cerrar items manualmente**: cerrar el issue o mergear el PR los mueve automáticamente a Terminado
- **Límite WIP**: máximo 2 items en **En proceso** por persona
- **Todo item en En proceso debe tener un Assignee**

---

## 7. Tarea de onboarding obligatoria

Para completar el onboarding debés realizar los siguientes pasos. **No se te dará acceso completo a los repositorios hasta completarlos.**

### Paso 1: Leé este documento completo ✅

(Estás haciéndolo ahora.)

### Paso 2: Completá tu planilla de disponibilidad individual

Tu planilla es el registro de los horarios acordados en los que te comprometés a estar en el laboratorio. Debe reflejar tu presencia real y **actualizarse ante cualquier cambio** de horario o modalidad.

1. Hacé un fork de este repositorio (`.github`)
2. Creá una rama: `feat/horario-<tu-usuario-github>`
3. Copiá el archivo [`disponibilidad/TEMPLATE.md`](disponibilidad/TEMPLATE.md) y renombralo como `disponibilidad/<tu-usuario-github>.md`
4. Completá la tabla con los horarios a los que te comprometés y el resto de los campos
5. Abrí un Pull Request a este repositorio con:
   - **Título**: `feat: disponibilidad horaria — @<tu-usuario-github>`
   - **Descripción**: completar el template del PR
   - **Reviewers**: `@utn-fra-lse/docentes`

> Si tu disponibilidad cambia en el futuro, abrí un nuevo PR actualizando tu archivo. El historial de Git queda como registro de los cambios acordados.

### Paso 3: Agregá tu nombre a la grilla pública de presencia

El archivo [`profile/README.md`](profile/README.md) contiene una tabla con todos los integrantes del laboratorio y sus bloques de presencia semanal. Esta grilla es la vista pública y consolidada de quién está en el lab en cada horario.

En el mismo PR del Paso 2 (misma rama), editá el `profile/README.md` y agregá tu nombre en los bloques horarios que correspondan a tu disponibilidad.

- Si en ese horario ya hay otras personas, agregá tu nombre separado por coma
- Si la celda está vacía, escribí tu nombre directamente

---

_Última actualización: junio 2026 — Para sugerencias, abrí un issue con el label `docs`._
