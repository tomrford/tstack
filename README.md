# tstack

My skills and workflows for maintaining lots of projects of varying scope, inspired by pstack, Matt Pocock's skills and gstack; intended to become a public ChatGPT plugin.
Starting with test authoring and validation guidance, then developing workflows from real use of dots and orchestrator chats.

## Install in Codex

```sh
codex plugin marketplace add tomrford/tstack --ref main
codex plugin add tstack@tstack
```

Start a new chat to use the installed skills.

## Update

After changes are pushed to `main`, refresh the installed copy:

```sh
codex plugin marketplace upgrade tstack
```

Start a new chat after updating. Updates track `main`; the manifest version stays at `0.1.0`.
