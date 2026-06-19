# Documentation Project Instructions

This folder contains the public Failpath documentation site built with Mintlify.

## Content rules

- Write for backend engineers adding observability to request, job, and webhook flows.
- Use active voice and second person.
- Use sentence case for headings.
- Use `Failpath` for the product, `failpath` for the CLI command, and `@failpath/sdk` for the SDK package.
- Format file names, commands, paths, package names, and environment variables as code.
- Do not document internal admin features or implementation details from the app unless they affect CLI, SDK, or ingestion behavior.

## Endpoint rules

- Public docs should treat `https://api.failpath.dev` as the default API endpoint.
- Mention `FAILPATH_DEV_ENDPOINT` only as a local development override for people working on the Failpath API itself.

## Mintlify rules

- Pages are MDX files with YAML frontmatter.
- Navigation and branding live in `docs.json`.
- Use Mintlify components only when they clarify a task or reference page.
