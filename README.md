Maintained by [Ankara Yazılım](https://github.com/Ankara-Software) | [Project page](https://ankarayazilim.org/acik-kaynak/eve-agent)

**Status: beta.** `bun run typecheck` and `bun run build` pass, and both tools were executed directly against real directories. The model loop and the HTTP channel were not run end to end because that needs a model credential. The project is built on the [eve](https://www.npmjs.com/package/eve) framework, which is itself in beta.

# eve-agent

A small agent app built on the eve framework. It answers questions about a project directory using two read-only tools.

## Türkçe

eve-agent, eve çatısı üzerine kurulmuş küçük bir ajan uygulamasıdır. Bir proje klasörü hakkındaki soruları iki salt okunur araçla yanıtlar: `get_workspace_stats` klasörün dosya sayısı, klasör sayısı, toplam boyutu ve paket adı/sürümünü verir; `check_dependencies` ise `package.json` içindeki bağımlılıkları, geliştirme bağımlılıklarını ve `engines` alanını listeler. Varsayılan model `anthropic/claude-sonnet-4.6` olup Vercel AI Gateway üzerinden ya da doğrudan sağlayıcı anahtarıyla çalışır. Proje beta aşamasındadır; araçlar doğrudan test edilmiştir, model döngüsü gerçek bir model anahtarıyla uçtan uca denenmemiştir.

## What is in the box

- `agent/agent.ts`: agent definition, model `anthropic/claude-sonnet-4.6`.
- `agent/instructions.md`: system instructions.
- `agent/tools/get_workspace_stats.ts`: file count, directory count, total bytes, and package name and version of a directory. Skips `node_modules`, `.git` and `target`, and stops at depth 5.
- `agent/tools/check_dependencies.ts`: reads `package.json` of a directory and returns the dependency and dev dependency names and counts, and the `engines` field.
- `agent/channels/eve.ts`: the built-in eve HTTP channel with `localDev()`, `vercelOidc()` and `placeholderAuth()`.

Both tools accept any directory path that the process can read; they do not restrict paths. Do not expose the agent to untrusted users without adding authentication and path restrictions.

## Requirements

- Node 24 (see `engines` in `package.json`) and [Bun](https://bun.sh)
- A model credential: `AI_GATEWAY_API_KEY` (or a `VERCEL_OIDC_TOKEN` from `vercel link`) for the default gateway model, or the provider key such as `ANTHROPIC_API_KEY` for a direct provider model id

## Usage

```bash
git clone https://github.com/Ankara-Software/eve-agent.git
cd eve-agent
bun install
bun run dev        # eve dev: local development server and terminal UI
```

Other scripts:

```bash
bun run typecheck  # tsgo
bun run build      # eve build, output in .output/
bun run start      # eve start
```

## Production authentication

`agent/channels/eve.ts` ends with `placeholderAuth()`, which does not allow browser requests in production. Replace it with your own auth provider before deploying anything beyond local use.

## Development

See [CONTRIBUTING.md](CONTRIBUTING.md), [SECURITY.md](SECURITY.md) and [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md). eve documentation is in `node_modules/eve/docs/` after `bun install`.

## License

MIT. Copyright (c) 2026 Anılcan Kara and Ankara Yazılım contributors.
