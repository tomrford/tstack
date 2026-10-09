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

## Verification skills

`create-verification-skill` builds a project-local verification skill and feature map. `maintain-verification-skill` checks that map against source and live behaviour. Invoke these skills explicitly; their upstream invocation settings are preserved.

Both skills and the creation skill's `references/feature-map-example/` directory are vendored from [Cursor's pstack](https://github.com/cursor/plugins/tree/ccb5507cec1546dc88135c1139c811e6c59115ba/pstack) at revision `ccb5507cec1546dc88135c1139c811e6c59115ba`. The only changes to the upstream files replace `.cursor/skills/` with `.agents/skills/` for Codex; the reference files are unchanged. They require no other pstack skills or principles. The reference commands describe an illustrative Notes app, not tools to install.

Creation needs repository access and a runnable project with suitable interaction and evidence tools. Maintenance also needs subagent support, an existing verification skill and feature map, and access to the mapped features. A changed maintenance pass produces one PR, so it needs Git and forge access to ship corrections. Project-specific credentials, devices and services depend on the target repository.

## Licence

tstack is [MIT licensed](LICENSE), copyright 2026 Tom Ford. The vendored pstack material is copyright 2026 Lauren Tan and retains its [upstream MIT notice](licenses/pstack-MIT.txt).
