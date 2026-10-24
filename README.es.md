# EveryInfra Analysis Skills

<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/hero-dark.svg">
    <source media="(prefers-color-scheme: light)" srcset="assets/hero-light.svg">
    <img alt="Ocho reseñas sintéticas se agrupan en problemas y elogios, cada porcentaje con su denominador, y la media de la muestra se compara con la valoración del anuncio con una nota." src="assets/hero-light.svg" width="100%">
  </picture>
</p>

<p align="center">
  <a href="https://github.com/everyinfra/analysis-skills/releases/latest"><img src="https://img.shields.io/badge/Descargar_la_última_versión-2F363D?style=for-the-badge&logo=github&logoColor=white" alt="Descargar la última versión"></a>
  <a href="https://github.com/everyinfra/analysis-skills/issues"><img src="https://img.shields.io/badge/Reportar_un_problema-2F363D?style=for-the-badge&logo=github&logoColor=white" alt="Reportar un problema"></a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/version-0.4.1-brightgreen" alt="version 0.4.1">
  <img src="https://img.shields.io/badge/license-Apache--2.0-brightgreen" alt="Apache-2.0">
  <img src="https://img.shields.io/badge/skills-6-brightgreen" alt="6 skills">
  <img src="https://img.shields.io/badge/modelo-el_tuyo-brightgreen" alt="model">
</p>

<p align="center"><a href="README.md">English</a> · <a href="README.zh-CN.md">简体中文</a> · <b>Español</b></p>

**Descarga gratuita. Usa tu propia herramienta de IA y tu propio modelo.**

EveryInfra Analysis Skills es la versión `0.4.1`, con licencia Apache-2.0. El paquete se puede descargar e instalar de forma gratuita. Incluye **seis** Skills de análisis: cuatro de dominio más una capa compartida de disciplina, **analysis-foundation**. No llama a un modelo, no incluye un proveedor de modelos y no requiere una clave de API ni dependencias en tiempo de ejecución. La herramienta de IA compatible del cliente proporciona el modelo y la cuota del modelo.

Una llamada aparte a la API o MCP de recopilación de datos de EveryInfra puede generar cargos. La instalación gratuita de Skills no es una recopilación gratuita.

## Skills

| Slug | Qué analiza |
| --- | --- |
| `ecommerce-product-analysis` | Candidatos de producto a partir de CSV/JSON proporcionados por el usuario o de resultados ya obtenidos. |
| `social-content-performance` | Contenido social para una muestra y una ventana temporal indicadas, a partir de archivos proporcionados o de resultados ya obtenidos. |
| `content-analysis-tagging` | Registros etiquetados con una taxonomía proporcionada por el usuario o acordada. |
| `spreadsheet-deliverable` | Editable .xlsx workbooks with live formulas (inputs/calculations/outputs separated, recalculation and error scan, built-in checks, assumptions with sources) |
| `analysis-foundation` | **Capa de disciplina compartida**: pipeline de cuatro pasos, números solo desde código, denominadores nombrados, sin tasas con n<30, incertidumbre, redacción causal, tabla de gráficos, notas de método, calibración de etiquetado LLM. |
| `review-insights` | Problemas, elogios y patrones de calificación en reseñas de productos, apps, lugares o empresas, a partir de archivos proporcionados o de resultados ya obtenidos. |

Cada Skill analiza archivos proporcionados o resultados ya obtenidos. Instalar un Skill no recopila datos.

## Uso con datos de EveryInfra

Cada Skill también analiza resultados que ya obtuviste de EveryInfra. Ejemplos de acciones de EveryData compatibles (el catálogo en vivo muestra las acciones y los campos actuales):

| Skill | Acciones de EveryData de ejemplo |
| --- | --- |
| `ecommerce-product-analysis` | `amazon/search`, `aliexpress/search`, `taobao/search`, `jd/search`, `shopee/search` |
| `social-content-performance` | `tiktok/search`, `tiktok/user_videos`, `youtube/search`, `xiaohongshu/search`, `bilibili/search` |
| `content-analysis-tagging` | Registros de texto, por ejemplo `xiaohongshu/search`, `reddit/search`, `zhihu/search` o resultados `comments` |
| `review-insights` | `amazon/reviews`, `walmart/reviews`, `taobao/reviews`, `trustpilot/reviews`, `app_store/reviews`, `google_maps_reviews/reviews` |

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
| <img src="assets/icons/codex.svg" width="16" height="16" alt=""> Codex CLI / IDE   | `~/.agents/skills/`           |
| <img src="assets/icons/claude.svg" width="16" height="16" alt=""> Claude Code       | `~/.claude/skills/`           |

Copia una o más de estas carpetas de Skill exactas en `~/.agents/skills/` o `~/.claude/skills/`:

- `skills/ecommerce-product-analysis`
- `skills/social-content-performance`
- `skills/content-analysis-tagging`
- `skills/review-insights`
- `skills/spreadsheet-deliverable`

Copia también `skills/analysis-foundation`: todas las Skills la enlazan como capa compartida de disciplina. Los hosts compatibles pueden usar la carpeta de Skill indicada en su documentación.

<img src="assets/icons/codex.svg" width="16" height="16" alt=""> Codex CLI / IDE: `$ecommerce-product-analysis` · `$social-content-performance` · `$content-analysis-tagging` · `$review-insights`

<img src="assets/icons/claude.svg" width="16" height="16" alt=""> Claude Code: `/ecommerce-product-analysis` · `/social-content-performance` · `/content-analysis-tagging` · `/review-insights`

Para un ejemplo sintético, proporciona al modelo solo `source_response` y `task`; mantén `expected_output` fuera de la entrada del modelo para compararlo después.

[Build skills — <img src="assets/icons/codex.svg" width="16" height="16" alt=""> Codex](https://developers.openai.com/codex/build-skills) · [Extend <img src="assets/icons/claude.svg" width="16" height="16" alt=""> Claude with skills](https://code.claude.com/docs/en/skills)

## Fixtures sintéticos

El directorio `examples/` contiene cuatro fixtures sintéticos, uno por Skill. Son sintéticos:

- `examples/ecommerce-product-analysis.synthetic.json`
- `examples/social-content-performance.synthetic.json`
- `examples/content-analysis-tagging.synthetic.json`
- `examples/review-insights.synthetic.json`

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
