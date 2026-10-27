# vetting-external-skills

> Tratar cada skill, plugin o MCP externo como código de un desconocido.

**Evaluar skills de terceros** · Skill para agentes de código de la comunidad [nvvdev](https://github.com/nvv-dev). Funciona en Claude Code como plugin o como skill suelta, y en cualquier agente compatible con el formato abierto [`SKILL.md`](https://agentskills.io).

*English summary at the end.*

## Qué hace

Proceso para decidir si instalar una skill, plugin, subagente, hook o servidor MCP de terceros: leerlo sin ejecutarlo, escanearlo con SkillSpector, revisar si duplica algo o cuesta muchos tokens, fijarlo a un commit exacto, registrarlo en un lockfile y dar atribución si se adapta.

## Objetivo

Que nada entre a tus agentes sin revisión, y que una actualización no se cuele sin volver a revisarla.

## Cuándo usarla

- Antes de instalar, copiar o actualizar cualquier skill, plugin o MCP externo

## Cuándo no

- Herramientas oficiales ya aprobadas y fijadas

## Ejemplo

```text
Evalúa si podemos instalar el repo github.com/owner/some-skill.
```

## Cómo se activa

Esta skill **se activa sola**: Claude Code lee su descripción y la carga cuando la tarea coincide. También puedes pedirla por nombre ("usa la skill vetting-external-skills") o invocarla con `/vetting-external-skills:vetting-external-skills` (plugin) o `/vetting-external-skills` (copiada a `.claude/skills/`).

## Instalación

### Opción 1: Claude Code, como plugin (recomendada)

Dentro de Claude Code:

```text
/plugin marketplace add nvv-dev/claude-plugins
/plugin install vetting-external-skills@nvvdev
```

La primera línea agrega el catálogo de nvvdev una sola vez; la segunda instala esta skill. Si prefieres el paquete completo, instala `agent-guardrails@nvvdev` en su lugar (incluye esta skill y las demás de [agent-guardrails](https://github.com/nvv-dev/agent-guardrails)); no instales los dos a la vez.

### Opción 2: Claude Code, copiando la skill

Para un solo proyecto (se comparte con tu equipo por git):

```bash
git clone --depth 1 https://github.com/nvv-dev/vetting-external-skills.git /tmp/vetting-external-skills
mkdir -p .claude/skills
cp -R /tmp/vetting-external-skills/skills/vetting-external-skills .claude/skills/
```

Para todos tus proyectos, cópiala en `~/.claude/skills/` en lugar de `.claude/skills/`.

### Opción 3: otros agentes

Copia la carpeta `skills/vetting-external-skills/` en la carpeta de skills de tu agente (cada agente documenta la suya). Con la CLI [skills](https://github.com/vercel-labs/skills) de Vercel Labs:

```bash
DISABLE_TELEMETRY=1 npx skills add nvv-dev/vetting-external-skills
```

### Verificar

Abre una sesión nueva y pregunta "¿qué skills tienes disponibles?"; `vetting-external-skills` debe aparecer. Con el plugin, `/plugin` la muestra como instalada.

### Actualizar o desinstalar

- Plugin: `/plugin marketplace update nvvdev` para actualizar; `/plugin uninstall vetting-external-skills@nvvdev` para quitarla.
- Copia manual: repite la copia para actualizar, o borra la carpeta `.claude/skills/vetting-external-skills`.

Antes de instalar cualquier skill, incluida esta, conviene leerla: es un solo archivo, [`skills/vetting-external-skills/SKILL.md`](skills/vetting-external-skills/SKILL.md). Ver [vetting-external-skills](https://github.com/nvv-dev/vetting-external-skills).

## Contenido

| Ruta | Qué es |
|---|---|
| `skills/vetting-external-skills/SKILL.md` | La skill: instrucciones en inglés para que los escáneres de seguridad las analicen completas; el agente responde en tu idioma |
| `.claude-plugin/plugin.json` | Manifiesto para instalarla como plugin |
| `.github/workflows/` | Validación de estructura y escaneo con SkillSpector en cada cambio |

## Contribuir

Este repo se **genera** desde [nvv-dev/agent-guardrails](https://github.com/nvv-dev/agent-guardrails), donde vive la versión canónica. Abre issues y PRs allí. La mejor contribución es un caso real en la sección *Known failures* de la skill, con la regla que lo evita.

## Origen

Escrita desde cero por nvvdev. Inspirada en: [NVIDIA/SkillSpector](https://github.com/NVIDIA/SkillSpector) (used as an external tool), [vercel-labs/skills](https://github.com/vercel-labs/skills) (pinned lockfile idea), [Hainrixz/claude-webkit](https://github.com/Hainrixz/claude-webkit) (attribution practice).

## Licencia

MIT.

---

## English

**vetting-external-skills** — Read without running, SkillSpector scan, fit and cost check, pin to a commit, record in a lockfile, credit the source.

Install in Claude Code with `/plugin marketplace add nvv-dev/claude-plugins` and `/plugin install vetting-external-skills@nvvdev`, or copy `skills/vetting-external-skills/` into `.claude/skills/` (project) or `~/.claude/skills/` (personal). Other agents: copy the folder into their skills directory, or run `DISABLE_TELEMETRY=1 npx skills add nvv-dev/vetting-external-skills`. Loads automatically when the task matches its description. Canonical source: [nvv-dev/agent-guardrails](https://github.com/nvv-dev/agent-guardrails). License: MIT.
