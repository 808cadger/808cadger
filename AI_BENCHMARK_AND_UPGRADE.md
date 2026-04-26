# AI App Benchmark and Upgrade Plan

Date: 2026-04-26

## Benchmarked leaders

| Project | Current signal | What they do well |
| --- | ---: | --- |
| Dify | 139k+ stars | Agent workflows, RAG, tool catalogs, model management, observability, API-first deployment |
| Open WebUI | 134k+ stars | Multi-provider chat UI, local/offline model support, extensible user experience |
| LangChain | 135k+ stars | Agent engineering primitives, tool orchestration, production integrations |
| AnythingLLM | 59k+ stars | Privacy-first setup, local/on-device positioning, workspace knowledge |
| Flowise | 52k+ stars | Visual agent builder, workflow automation, low-code agent composition |
| LobeChat | 69k+ stars | Polished AI chat UX, multi-provider support, knowledge base, multimodal/plugin surface |

## Portfolio gap analysis

| Area | Current portfolio | Upgrade target |
| --- | --- | --- |
| AI entry point | Many apps have chat/avatar, but implementations differ by repo | Shared agentic avatar widget with domain roles and skill chips |
| Agent behavior | Strong domain prompts in several apps, deeper pipelines in RepairPro | Standard skill taxonomy: assess, draft, plan, route, triage, explain, report |
| Tool routing | Some apps have explicit backend agents; most static apps only chat | Browser event hook so each app can attach real tools without changing avatar UI |
| Provider strategy | Mostly direct Anthropic calls or app-specific backend routes | Widget supports app backend endpoint first, then local Anthropic fallback |
| Safety posture | Privacy-first messaging exists, but direct browser calls remain | Clear demo mode, short bounded prompts, domain guardrails, no silent data capture |
| UX polish | Floating avatar exists in many apps | Consistent avatar, mobile panel, quick skills, domain colors, accessible controls |

## Implemented first upgrade

Added a reusable agentic avatar layer across the static/PWA apps. The widget now:

- Detects app domain from metadata/context.
- Switches avatar role and skills for legal, farm, repair, travel, skin, shopping, fraud, and general apps.
- Shows visible skill buttons instead of a generic chat-only prompt.
- Emits `sw-avatar:skill` events so each app can bind real workflows later.
- Uses `window.SWAvatarEndpoint` when an app provides a backend chat/agent endpoint.
- Falls back to Anthropic direct browser calls only when no endpoint is configured.
- Provides demo-mode answers when no API key is present.
- Keeps answers short and domain-guardrailed.

## Next upgrades

1. Add app-specific handlers for `sw-avatar:skill` in the strongest repos first:
   RepairPro, CourtAide, FarmSense, GlowAI, time-save-shopping, HaloGuard.
2. Move browser-direct AI calls behind backend endpoints where the repo already has FastAPI.
3. Add one small knowledge file per app so the avatar can answer product-specific questions offline.
4. Add smoke tests that assert every shipped HTML entry point contains `#sw-avatar` and loads `avatar-widget.js`.
5. Add a public portfolio section showing benchmarked differentiators: agent skills, privacy posture, local-first install, and multi-platform deployment.
