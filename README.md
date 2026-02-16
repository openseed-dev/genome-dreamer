# genome-dreamer

The default [OpenSeed](https://github.com/openseed-dev/openseed) genome — a full cognitive architecture with dreams, memory consolidation, self-evaluation, and a persistent browser.

## What It Does

Creatures with the dreamer genome can:

- **Think and act** — continuous LLM conversation loop with bash and browser tools
- **Dream** — consolidate memories into prioritized observations and behavioral rules during sleep
- **Self-evaluate** — a separate Creator agent reviews the creature's state every 10th sleep and may modify its source code
- **Browse the web** — persistent headless Chromium session with anti-detection
- **Manage fatigue** — forced consolidation after 80 actions per wake cycle

## Install

Already bundled with OpenSeed. Or install explicitly:

```bash
seed genome install dreamer
```

## Use

```bash
seed spawn eve --genome dreamer --purpose "find purpose"
```

Since dreamer is the default genome, `--genome dreamer` is optional.

## Fork It

The best way to build a custom genome is to fork this repo:

1. Fork this repo on GitHub
2. Modify the cognitive architecture in `src/mind.ts`
3. Update `genome.json` with your genome's name, description, and tabs
4. Install your genome: `seed genome install your-username/genome-your-name`
5. Spawn a creature with it: `seed spawn scout --genome your-name`

## Structure

```
genome.json          manifest — name, version, tabs, validation command
package.json         dependencies (ai sdk, playwright, zod, tsx)
Dockerfile           creature container image
PURPOSE.md           template purpose file (overwritten at spawn time)
tsconfig.json        TypeScript config
src/
  index.ts           entry point — HTTP server, creature lifecycle
  mind.ts            cognitive core — LLM loop, dreams, consolidation, self-eval
  memory.ts          JSONL-based working memory
  tools/
    bash.ts          bash execution with temp-file I/O
    browser.ts       persistent headless Chromium
```

## genome.json

```json
{
  "name": "dreamer",
  "version": "0.1.0",
  "description": "Full cognitive architecture with dreams, memory consolidation, self-evaluation, and persistent browser.",
  "requires": { "openseed": ">=0.0.1" },
  "tabs": [
    { "id": "purpose", "label": "purpose", "file": "PURPOSE.md", "type": "markdown" },
    { "id": "diary", "label": "diary", "file": "self/diary.md", "type": "markdown" },
    { "id": "observations", "label": "observations", "file": ".self/observations.md", "type": "text" },
    { "id": "rules", "label": "rules", "file": ".self/rules.md", "type": "text" },
    { "id": "dreams", "label": "dreams", "file": ".self/dreams.jsonl", "type": "jsonl", "limit": 10 },
    { "id": "self-eval", "label": "self-eval", "file": ".self/creator-log.jsonl", "type": "jsonl", "limit": 10 }
  ]
}
```

## License

MIT
