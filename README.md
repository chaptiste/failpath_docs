# Failpath Documentation

This is the Mintlify source for the public Failpath docs site.

## Local preview

Install the Mintlify CLI, then run it from this folder:

```sh
npm i -g mint
cd failpath_docs
mint dev
```

The local preview runs at [http://localhost:3000](http://localhost:3000).

## Structure

- `introduction.mdx` and `quickstart.mdx` introduce the product and first setup flow.
- `concepts/` explains flows, runs, steps, and events.
- `cli/` documents the `failpath` command line tool.
- `sdk/` documents `@failpath/sdk`.
- `guides/` contains task-focused instrumentation and environment guides.
- `docs.json` controls navigation, theme, logo, and Mintlify settings.

## Writing rules

- Use second person and active voice.
- Keep headings sentence case.
- Use `Failpath` for the product, `failpath` for the CLI command, and `@failpath/sdk` for the package.
- Keep production endpoint guidance clear: normal users should rely on the default `https://api.failpath.dev`; `FAILPATH_DEV_ENDPOINT` is only for local API development.
