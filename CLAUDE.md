# Coders University — landing

Single-file static site (`index.html`) com Hero, Pain points, Faculty, Stats, ESIC, Programas, Portfolio, Market, FAQ e CTAs. Deploy via Vercel.

## Fontes

A landing usa **NexaText** (Adobe Fonts) com **Inter** + system fonts como fallback.

- O kit do Typekit é carregado em `<head>`:
  ```html
  <link rel="preconnect" href="https://use.typekit.net" crossorigin>
  <link rel="preconnect" href="https://p.typekit.net" crossorigin>
  <link rel="stylesheet" href="https://use.typekit.net/lxp1meo.css" media="print" onload="this.media='all'">
  <noscript><link rel="stylesheet" href="https://use.typekit.net/lxp1meo.css"></noscript>
  ```
  O truque `media="print"` + `onload` carrega o CSS sem bloquear o primeiro paint; o `<noscript>` é fallback se JS estiver desligado.

- O nome real declarado pelo kit é **`"nexa-text"`** (kebab-case). Em todo o CSS use sempre:
  ```css
  font-family: "nexa-text", "Inter", sans-serif;
  ```
  **Nunca** use `"NexaText"` ou `"Nexa Text"` — não bate com o `@font-face` do Adobe e cai pro fallback.

- **Performance/swap**: pra evitar FOIT (texto invisível enquanto baixa), o kit precisa estar configurado com `font-display: swap` no painel da Adobe Fonts (https://fonts.adobe.com → seu kit → settings → "Default font-display value" = swap). Isso é configuração externa — não tem como forçar via CSS local.

- **Pesos disponíveis no kit**: 400, 500, 700 (italic + non-italic). Se o CSS pedir 600, o browser sintetiza (renderiza falso-bold). Se quiser evitar, use 500 ou 700 explícitos onde tiver 600.

## Regras de execução

- **Antes de qualquer operação git destrutiva** (`git restore`, `git reset --hard`, `git checkout --`, force push, branch -D, clean -f) — **PARE e confirme com o usuário**. Não usar atalho destrutivo pra reverter mudança recente: usar Edit/Read manualmente ou `git stash` primeiro.
- **Não rodar `perl -i`/`sed -i` no `index.html` sem testar primeiro em uma linha isolada**. Cuidado especial com syntax: perl usa `$1`/`$2` pra capture groups (não `\1`/`\2` — esses viram escapes octais e corrompem o arquivo).
- **Mudanças de fonte**: confirmar que `font-family` usa o nome real do kit (`"nexa-text"`), não o display name (`"NexaText"`).

## Estrutura

- `index.html` — landing inteira (HTML + CSS inline + JS inline)
- `assets/` — imagens (avif), SVGs, logo, mapa, fontes locais (não tem)
- Deploy: Vercel (vercel.json + .vercelignore filtram refs/, copy/ etc)
