# Source: https://www.npmjs.com/package/failpath

# failpath

0.1.2 • Public • Published 3 days ago

- [Readme](https://www.npmjs.com/?activeTab=readme)
- [Code Beta](https://www.npmjs.com/?activeTab=code)
- [0 Dependencies](https://www.npmjs.com/?activeTab=dependencies)
- [0 Dependents](https://www.npmjs.com/?activeTab=dependents)
- [3 Versions](https://www.npmjs.com/?activeTab=versions)

# Failpath CLI

Initialize a repository for Failpath, pull dashboard graphs into `.failpath/flows.json`, and publish local edits back to Failpath.

```shell
npx failpath init --project-key fp_project_xxx
npx failpath publish
npx failpath sync
```

## Commands

- `init`: creates `.env`, updates `.gitignore`, creates `.failpath/AGENTS.md`, and pulls the configured project's current dashboard graph into `.failpath/flows.json`.
- `sync`: pulls dashboard graph edits into `.failpath/flows.json`.
- `publish`: validates `.failpath/flows.json` and pushes local edits to Failpath.

## Environment

- `FAILPATH_PROJECT_KEY`: project key written to `.env` by `init` and read by `publish` and `sync`.

## Development

The Failpath API endpoint defaults to `https://api.failpath.dev`. For local API development only, pass `--endpoint` to `init`, `publish`, or `sync`, or set `FAILPATH_DEV_ENDPOINT` in your shell.

## Readme

### Keywords

none