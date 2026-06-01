# Skill Teaching Programming

[Leer este README en inglés](./README.md)

`teaching-programming` es un skill solo de instrucciones para sesiones de programación en las que la persona quiere aprender mientras el agente implementa.

Convierte al asistente en un profesor paso a paso: hacer un cambio pequeño, mostrar el cambio, explicar el motivo y recién después continuar.

## Estado

Versión actual: `0.1.0`

Esta es la primera versión pública del skill. Ya está lista para probarse e iterarse, pero las instrucciones pueden seguir evolucionando según el uso real.

Las notas de versiones publicadas viven en [`CHANGELOG.md`](./CHANGELOG.md).

## Autoría y licencia

Copyright (c) 2026 Sergio Alonso.

Licenciado bajo `AGPL-3.0-or-later`. Ver [`LICENSE`](./LICENSE).

## Camino rápido

1. Instalá el skill con el CLI de `skills`, o copiá manualmente el `SKILL.md` canónico si hace falta.
2. Pedile al agente que enseñe mientras programa, por ejemplo: `Enseñame mientras agregas validación a esta función.`
3. Verificá que el agente cambie a pasos pequeños de enseñanza en vez de volcar una solución completa de una sola vez.

## Qué exige este skill

Cuando está activo, el asistente debe:

- trabajar en pasos pequeños de enseñanza
- detenerse después de cambios lógicos significativos
- mostrar la ruta absoluta completa de cada archivo modificado
- mostrar un diff contextual siempre que sea posible
- incluir 5 líneas antes y 5 líneas después de la región modificada siempre que sea posible
- explicar qué cambió, por qué cambió, qué concepto de programación está involucrado y qué pasaría si no se hiciera
- terminar con un resumen corto de aprendizaje

También debería:

- preguntar antes de salir del modo enseñanza para pasar a un modo de implementación más rápido
- reducir las explicaciones de sintaxis básica una vez que la persona ya la entiende
- preservar la corrección y evitar reescrituras demasiado grandes

## Buenos ejemplos de activación

Español:

- `enseñame`
- `enséñame`
- `explicame mientras programas`
- `explícame mientras programas`
- `paso a paso`
- `modo enseñanza`

English:

- `teach me`
- `step by step`
- `explain while coding`
- `teaching mode`
- `walk me through it`

## Comportamiento esperado

Si la persona dice:

```text
Enseñame mientras agregas validación a esta función.
```

el asistente debería:

1. activar el modo enseñanza
2. cambiar primero una parte significativa
3. mostrar la ruta completa del archivo
4. mostrar la región cambiada con contexto alrededor
5. explicar el cambio antes de seguir

## Contenido del repositorio

```text
learn-by-coding-skill/
├── CHANGELOG.md
├── .gitignore
├── LICENSE
├── README.md
├── README-es.md
├── skills.sh.json
└── skills/
    └── teaching-programming/
        └── SKILL.md
```

Notas:

- `skills/teaching-programming/SKILL.md` es el archivo canónico de instrucciones runtime.
- `README.md` explica intención, instalación y verificación en inglés.
- `README-es.md` ofrece la misma guía general en español.
- `CHANGELOG.md` registra el historial de versiones publicadas.
- `skills.sh.json` personaliza cómo puede verse la página del repositorio en skills.sh.
- `.atl/` se considera estado local del entorno y está excluido intencionalmente del repo publicado.

## Nombre canónico del skill

Usá exactamente este nombre de carpeta al instalar el skill:

```text
teaching-programming
```

## Instalar con el CLI de skills

Este es el camino más alineado con el ecosistema para agentes compatibles con skills.sh:

```bash
npx skills add https://github.com/perfeccion-ar/learn-by-coding-skill --skill teaching-programming
```

Por qué importa este camino:

- coincide con el patrón de instalación que muestran las páginas de skills.sh
- hace que el repo sea más fácil de instalar para agentes compatibles
- es el camino de instalación que contribuye al descubrimiento y a la telemetría del leaderboard de skills.sh

## Instalación manual

Si no estás usando el CLI de `skills`, la regla portable es simple: colocá el `SKILL.md` canónico dentro de una carpeta llamada `teaching-programming` en el lugar donde tu agente descubra skills.

### OpenCode

Si tu instalación de OpenCode descubre skills desde carpetas estándar de proyecto o globales, este es el layout esperado:

Proyecto local:

```bash
mkdir -p .opencode/skills/teaching-programming
cp skills/teaching-programming/SKILL.md .opencode/skills/teaching-programming/SKILL.md
```

Global:

```bash
mkdir -p ~/.config/opencode/skills/teaching-programming
cp skills/teaching-programming/SKILL.md ~/.config/opencode/skills/teaching-programming/SKILL.md
```

### Carpetas de skill estilo Claude

Para carpetas de skill estilo Claude, este es un layout común:

Proyecto local:

```bash
mkdir -p .claude/skills/teaching-programming
cp skills/teaching-programming/SKILL.md .claude/skills/teaching-programming/SKILL.md
```

Global:

```bash
mkdir -p ~/.claude/skills/teaching-programming
cp skills/teaching-programming/SKILL.md ~/.claude/skills/teaching-programming/SKILL.md
```

### Herramientas basadas en AGENTS.md

Si tu herramienta no descubre `SKILL.md` automáticamente, guardá el skill en una carpeta del proyecto y referencialo desde `AGENTS.md` o desde un archivo equivalente de instrucciones.

```bash
mkdir -p .agents/skills/teaching-programming
cp skills/teaching-programming/SKILL.md .agents/skills/teaching-programming/SKILL.md
```

Después apuntá tu `AGENTS.md` a:

```text
.agents/skills/teaching-programming/SKILL.md
```

### Carga directa por ruta

Si tu agente soporta pasar una ruta de skill directamente, guardá el archivo en un lugar estable:

```bash
mkdir -p ~/ai-skills/teaching-programming
cp skills/teaching-programming/SKILL.md ~/ai-skills/teaching-programming/SKILL.md
```

Después cargá:

```text
~/ai-skills/teaching-programming/SKILL.md
```

## Layout de proyecto recomendado

```text
my-project/
├── AGENTS.md
├── .agents/
│   └── skills/
│       └── teaching-programming/
│           └── SKILL.md
├── .opencode/
│   └── skills/
│       └── teaching-programming/
│           └── SKILL.md
└── .claude/
    └── skills/
        └── teaching-programming/
            └── SKILL.md
```

No necesitás tener todas las copias salvo que quieras compatibilidad amplia.

## Prompt de verificación

Después de instalarlo, probalo con:

```text
Enseñame mientras creas una función simple que reciba una lista de números y devuelva la suma de los números pares. Detente después de crear la función, después del bucle y después del if.
```

Resultado esperado:

- el agente reconoce el modo enseñanza
- evita una solución única grande y sin explicación
- muestra rutas de archivo y diffs contextuales
- explica la función, el bucle y la condición
- termina con un resumen corto de aprendizaje

## Alcance y límites

- Este es un skill solo de instrucciones.
- No ejecuta código ni instala dependencias por sí mismo.
- Es seguro de inspeccionar porque su comportamiento está definido en Markdown plano.
- La fuente de verdad runtime es `skills/teaching-programming/SKILL.md`.
- El comportamiento exacto de descubrimiento depende de cada herramienta, así que verificá rutas y reglas de carga en tu agente antes de expandir su uso.
- El descubrimiento en skills.sh depende de instalaciones reales con el CLI de `skills` y puede tardar en aparecer porque las páginas del repositorio se cachean.
