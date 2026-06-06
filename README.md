# claudeenv-demo-project

A sample project for trying out [`claudeenv`](https://github.com/nemethk/claudeenv) — paired
with [`claudeenv-demo-profiles`](https://github.com/nemethk/claudeenv-demo-profiles), which
supplies the skills, agents, and rules this project loads.

## What's here

A fake Go + Kubernetes service (`payment-service`) with `.claudeenv` already committed
at the repo root:

```ini
[project]
golang
kubernetes

[global]
programming
```

This is exactly what a real repo looks like once a team adopts `claudeenv` — the profile
selection travels with the code, so anyone who clones it gets the right Claude Code tools
automatically, with no extra setup beyond pointing `CLAUDEENV_DIR_*` at a profiles repo.

## Run the demo

Clone this repo and the profiles repo side by side, point `claudeenv` at the profiles, then load:

```bash
git clone git@github.com:nemethk/claudeenv-demo-project.git
git clone git@github.com:nemethk/claudeenv-demo-profiles.git

export CLAUDEENV_DIR_PROJECT=$(pwd)/claudeenv-demo-profiles/claude-project
export CLAUDEENV_DIR_GLOBAL=$(pwd)/claudeenv-demo-profiles/claude-global

cd claudeenv-demo-project
claudeenv global use programming
claudeenv load
```

`claudeenv load` symlinks the `golang` + `kubernetes` profiles' `skills/`, `agents/`, `rules/`
into `.claude/`, and the `programming` profile into `~/.claude/`. Run `claude` from this
directory afterwards — you'll see only Go and Kubernetes tools, none of the unrelated noise
a flat, profile-less setup would show.

## Reset

```bash
claudeenv project reset    # removes .claudeenv
claudeenv global reset     # removes the global symlinks + state.json entry
```

## Related

- [`claudeenv`](https://github.com/nemethk/claudeenv) — the tool this project demos
- [`claudeenv-demo-profiles`](https://github.com/nemethk/claudeenv-demo-profiles) — the profiles this project's `.claudeenv` references
