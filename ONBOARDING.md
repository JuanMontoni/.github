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
6. [Uso de GitHub Projects (Kanban + Scrum)](#6-uso-de-github-projects-kanban--scrum)
7. [Team Discussions](#7-team-discussions)
8. [Tarea de onboarding obligatoria](#8-tarea-de-onboarding-obligatoria)

---

## 1. Roles

La organización maneja tres roles principales. Cada uno tiene permisos distintos en los repositorios.

| Rol | Descripción | Permisos |
|-----|-------------|----------|
| **Docente** | Responsable técnico o académico de uno o más proyectos. Aprueba PRs y coordina sprints. | Write + Review en todos los repos |
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
| `develop` | Integración continua del sprint actual | PR obligatorio |

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
   - **Milestone**: sprint o entrega asociada

### Labels estándar

| Label | Color | Uso |
|-------|-------|-----|
| `bug` | rojo | Algo no funciona |
| `feature` | verde | Nueva funcionalidad |
| `docs` | azul claro | Documentación |
| `actividad-lab` | amarillo | Tarea operativa del laboratorio |
| `prioridad: alta` | naranja | Urgente |
| `prioridad: media` | amarillo | Normal |
| `prioridad: baja` | gris | Puede esperar |
| `bloqueado` | negro | Depende de otro issue |

### Ciclo de vida de un issue

```
Backlog → To Do (sprint planning) → In Progress → In Review → Done
```

Cuando empezás a trabajar en un issue, movelo a **In Progress** en el tablero y creá la rama correspondiente.

---

## 5. Pull Requests: cómo crearlos y gestionarlos

### Cuándo abrir un PR

Cuando una rama está lista para revisión. No esperes a tener todo perfecto: podés abrir un **Draft PR** mientras trabajás para visibilidad del equipo.

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
- Al menos **1 aprobación** de un docente para mergear a `develop`
- Al menos **1 aprobación** de un docente para mergear a `main`
- Los comentarios de revisión deben resolverse antes de mergear
- Usar **Squash and merge** para mantener limpio el historial de `main`

### Tipos de feedback en revisión

- ✅ **Approve**: listo para mergear
- 💬 **Comment**: observación sin bloqueo
- ❌ **Request changes**: requiere correcciones antes de aprobar

---

## 6. Uso de GitHub Projects (Kanban + Scrum)

### Estructura de tableros

La organización tiene dos tipos de tableros:

| Tablero | Alcance | Administrador |
|---------|---------|---------------|
| **Actividades Generales del Lab** | Tareas operativas, administrativas y transversales | Docentes |
| **[Nombre Proyecto]** | Issues y PRs del proyecto específico | Docente responsable del proyecto |

### Columnas Kanban

Todos los tableros usan las mismas columnas:

```
📥 Backlog  →  📋 To Do  →  🔧 In Progress  →  👀 In Review  →  ✅ Done
```

| Columna | Significado |
|---------|-------------|
| **Backlog** | Ideas y tareas no planificadas aún |
| **To Do** | Comprometidas para el sprint actual |
| **In Progress** | En trabajo activo (máx. 2 por persona) |
| **In Review** | PR abierto, esperando revisión |
| **Done** | Completadas y mergeadas |

### Campos personalizados de cada item

| Campo | Tipo | Uso |
|-------|------|-----|
| `Sprint` | Iteración | Sprint de Scrum asignado |
| `Estimación` | Número | Story points o horas estimadas |
| `Tipo` | Select | `Feature / Bug / Docs / Actividad` |
| `Prioridad` | Select | `Alta / Media / Baja` |

### Scrum en Projects

- **Sprint Planning**: al inicio de cada sprint, mover items de Backlog a To Do
- **Daily (opcional)**: actualizar el estado de los items en el tablero
- **Sprint Review**: revisar columna Done al cierre del sprint
- **Retrospectiva**: documentar en una discusión del team (ver sección 7)

### Reglas del tablero

- **No cerrar items manualmente**: cerrar el issue o mergear el PR los mueve automáticamente a Done
- **Límite WIP**: máximo 2 items en **In Progress** por persona
- **Todo item en In Progress debe tener un Assignee**

---

## 7. Team Discussions

Las Team Discussions son el espacio de comunicación interna por equipo. Se accede desde la organización → **Teams** → seleccionar el team → pestaña **Discussions**.

### Para qué usar discussions

| Uso | Ejemplo |
|-----|---------|
| Anuncios del lab | "El viernes no hay laboratorio" |
| Retrospectivas de sprint | "¿Qué salió bien / mal este sprint?" |
| Decisiones técnicas | "¿Usamos FreeRTOS o Zephyr?" |
| Consultas generales | "¿Alguien tiene experiencia con el sensor X?" |
| Bienvenidas | Post de presentación al unirse al team |

### Cuándo NO usar discussions

- Para reportar bugs o tareas → crear un **Issue**
- Para cambios de código → abrir un **PR**
- Para comunicación urgente → usar el canal de comunicación del lab (WhatsApp/Signal/etc.)

### Convenciones

- Usar un título claro y descriptivo
- Categorizar correctamente la discusión (Announcement / General / Ideas / Q&A)
- Mencionar al team completo con `@utn-fra-lse/docentes` o `@utn-fra-lse/becarios` cuando corresponda
- Las retrospectivas de sprint van en `@utn-fra-lse/docentes` con el formato: `Retrospectiva Sprint N — [Proyecto]`

---

## 8. Tarea de onboarding obligatoria

Para completar el onboarding debés realizar los siguientes pasos. **No se te dará acceso completo a los repositorios hasta completarlos.**

### Paso 1: Leé este documento completo ✅

(Estás haciéndolo ahora.)

### Paso 2: Completá tu disponibilidad horaria

1. Hacé un fork de este repositorio (`.github`)
2. Creá una rama: `feat/horario-<tu-usuario-github>`
3. Copiá el archivo [`disponibilidad/TEMPLATE.md`](disponibilidad/TEMPLATE.md) y renombralo como `disponibilidad/<tu-usuario-github>.md`
4. Completá la tabla de disponibilidad y el resto de los campos
5. Abrí un Pull Request a este repositorio con:
   - **Título**: `feat: disponibilidad horaria — @<tu-usuario-github>`
   - **Descripción**: completar el template del PR
   - **Reviewers**: `@utn-fra-lse/docentes`

### Paso 3: Publicá tu presentación en el Team Discussion

Ingresá al team al que pertenecés (`docentes` o `becarios`) y creá una nueva Discussion con:
- **Categoría**: General
- **Título**: `Presentación — Nombre Apellido`
- **Contenido**: breve presentación (rol, qué hacés, qué esperás del lab)

---

_Última actualización: junio 2026 — Para sugerencias, abrí un issue con el label `docs`._
