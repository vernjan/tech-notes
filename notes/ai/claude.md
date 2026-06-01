# Claude

- sessions can be rewinded, resumed and forked

## CLI

- `tail -200 app.log | claude -p "Look for any anomalies"` - using pipes
- `-p` - non-interactive prompt
- `-c` - continue the latest sessions
- `-r` - resume session (interactive list of options)

## Shortcuts

- `!` - shell mode
- `@` - file or folder references (e.g. `@vasa/` or `@deploy_vasa.sh:123`)
- `UP/DOWN` - navigate prompt history
- `ESC` - interrupt current task
- `ESC ESC` - rewind
- `shift + tab` - switch between permission modes
    - **default** — ask before every edit
    - **accept edits** — edit freely, ask for commands
    - **plan** — research and propose, never touch files
    - **auto** — Claude decides what is safe
- `alt + p` - switch model

## Commands

- `/init` - initialize new repo (creates `CLAUDE.md`)
- `/clear` - starts new session
- `/context` - show context window

## Tips

- `CLAUDE.md`
- `think" < "think hard" < "think harder" < "ultrathink`
