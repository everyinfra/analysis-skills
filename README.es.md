# EveryInfra Analysis Skills

[English](README.md) · [简体中文](README.zh-CN.md) · [Español](README.es.md)

**Descarga gratuita. Usa tu propia herramienta de IA y tu propio modelo.**

EveryInfra Analysis Skills es la versión `0.1.0`, con licencia Apache-2.0. El paquete se puede descargar e instalar de forma gratuita. Incluye tres Skills de análisis. No llama a un modelo, no incluye un proveedor de modelos y no requiere una clave de API ni dependencias en tiempo de ejecución. La herramienta de IA compatible del cliente proporciona el modelo y la cuota del modelo.

Una llamada aparte a la API o MCP de recopilación de datos de EveryInfra puede generar cargos. La instalación gratuita de Skills no es una recopilación gratuita.

## Skills

| Slug | Qué analiza |
| --- | --- |
| `ecommerce-product-analysis` | Candidatos de producto a partir de CSV/JSON proporcionados por el usuario o de resultados ya obtenidos. |
| `social-content-performance` | Contenido social para una muestra y una ventana temporal indicadas, a partir de archivos proporcionados o de resultados ya obtenidos. |
| `content-analysis-tagging` | Registros etiquetados con una taxonomía proporcionada por el usuario o acordada. |

Cada Skill analiza archivos proporcionados o resultados ya obtenidos. Instalar un Skill no recopila datos.

## Uso con datos de EveryInfra

Cada Skill también analiza resultados que ya obtuviste de EveryInfra. Ejemplos de acciones de EveryData compatibles (el catálogo en vivo muestra las acciones y los campos actuales):

| Skill | Acciones de EveryData de ejemplo |
| --- | --- |
| `ecommerce-product-analysis` | `amazon/search`, `walmart/search`, `taobao/search`, `jd/search`, `shopee/search` |
| `social-content-performance` | `tiktok/search`, `tiktok/user_videos`, `youtube/search`, `xiaohongshu/search`, `bilibili/search` |
| `content-analysis-tagging` | Registros de texto, por ejemplo `xiaohongshu/search`, `reddit/search`, `zhihu/search` o resultados `comments` |

Catálogo en vivo: `GET https://api.everyinfra.com/api/v1/social/catalog`.

## Inicio rápido

1. Elige el Skill para la tarea.
2. Descarga el ZIP del repositorio o clona `https://github.com/everyinfra/analysis-skills.git`. Instala la carpeta del Skill seleccionado en la ubicación de Skill documentada del host compatible. Este README nombra `~/.agents/skills/` y `~/.claude/skills/`.
3. Configura o selecciona el modelo del propio cliente en los ajustes del host de IA. Este paquete no configura el host ni proporciona una clave de modelo.
4. Abre el fixture sintético correspondiente. Entrega al Skill el `source_response` y la tarea del fixture. El fixture incluye `expected_output`; compara la estructura devuelta, no la redacción exacta del modelo. Este paso no realiza ninguna llamada de recopilación de datos de EveryInfra.
5. Para una nueva recopilación de datos, consulta la documentación vigente de la API/MCP. La recopilación es un paso aparte y puede generar cargos.

## Descarga

Obtén el ZIP del código fuente del repositorio desde la página del repositorio de GitHub:

1. Abre [https://github.com/everyinfra/analysis-skills](https://github.com/everyinfra/analysis-skills).
2. Usa GitHub **Code** → **Download ZIP**.
3. Descomprime el ZIP.

O clona `https://github.com/everyinfra/analysis-skills.git`.

## Instalación

| Host              | Directorio de instalación     |
|-------------------|-------------------------------|
| Codex CLI / IDE   | `~/.agents/skills/`           |
| Claude Code       | `~/.claude/skills/`           |

Copia una o más de estas carpetas de Skill exactas en `~/.agents/skills/` o `~/.claude/skills/`:

- `skills/ecommerce-product-analysis`
- `skills/social-content-performance`
- `skills/content-analysis-tagging`

Cada carpeta de Skill se puede instalar de forma independiente. Los hosts compatibles pueden usar la carpeta de Skill indicada en su documentación.

Codex CLI / IDE: `$ecommerce-product-analysis` · `$social-content-performance` · `$content-analysis-tagging`

Claude Code: `/ecommerce-product-analysis` · `/social-content-performance` · `/content-analysis-tagging`

Para un ejemplo sintético, proporciona al modelo solo `source_response` y `task`; mantén `expected_output` fuera de la entrada del modelo para compararlo después.

[Build skills — Codex](https://developers.openai.com/codex/build-skills) · [Extend Claude with skills](https://code.claude.com/docs/en/skills)

## Fixtures sintéticos

El directorio `examples/` contiene tres fixtures sintéticos, uno por Skill. Son sintéticos:

- `examples/ecommerce-product-analysis.synthetic.json`
- `examples/social-content-performance.synthetic.json`
- `examples/content-analysis-tagging.synthetic.json`

Abre el fixture correspondiente y entrega al Skill el `source_response` y la tarea del fixture. Cada fixture incluye `expected_output`. Compara la estructura devuelta, no la redacción exacta del modelo. Usar un fixture no realiza ninguna llamada de recopilación de datos de EveryInfra.

## Recopilación y API pública

El análisis en estas Skills no genera cargos de Skill. La recopilación a través de la API o MCP de EveryInfra es un paso aparte y puede generar cargos. Consultar el catálogo o descubrir herramientas no autoriza una llamada de datos con cargo.

Referencias de la API pública:

- [https://api.everyinfra.com/docs](https://api.everyinfra.com/docs)
- [https://api.everyinfra.com/openapi.json](https://api.everyinfra.com/openapi.json)

## Mantenimiento y comentarios

Responsable de mantenimiento: EveryInfra (la organización).

Disparadores de actualización: cambios en el contrato o schema de la API pública, una corrección verificada de un Skill o ejemplo, o una solicitud de usuario aceptada. En cada actualización de versión del paquete, revisa los comentarios abiertos antes de cambiar la versión del manifiesto y el registro de cambios. Es una cadencia manual impulsada por eventos.

Canal de comentarios: GitHub Issues público en [https://github.com/everyinfra/analysis-skills/issues](https://github.com/everyinfra/analysis-skills/issues). No publiques claves de API, credenciales, registros privados de clientes u otros datos confidenciales.

## Licencia

Apache-2.0. Véase `LICENSE`.
