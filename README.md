# AI Agent Skills

A collection of model-agnostic skills for AI coding agents working with and contributing to Payload.

These skills package repeatable workflows, project knowledge, and helper scripts so contributors can install the same guidance across different agent runtimes.

## Installation

### Version-matched Payload skill (recommended)

Newer Payload releases ship this skill inside the `payload` npm package. Prefer that copy for application development because its guidance was released with the version of Payload installed in the project.

Check whether the installed package includes it:

```bash
test -f node_modules/payload/skills/payload/SKILL.md
```

Agents do not automatically discover skills under `node_modules`. For an existing project, add this pointer to the project instruction file your agent reads, such as `AGENTS.md` or `CLAUDE.md`:

```md
# AI Agent

Before performing any Payload-related work, read and follow `node_modules/payload/skills/payload/SKILL.md`.
Treat that bundled skill as authoritative for the installed Payload version.
```

In a monorepo, point to the `node_modules/payload` belonging to the workspace that contains the Payload application. Projects created by a compatible version of `create-payload-app` receive agent instruction files automatically.

After confirming the bundled file exists and adding the pointers, remove or disable any standalone `payload` skill already installed for the project.

### Standalone legacy fallback

Use this repository only when the installed `payload` package does not contain `skills/payload/SKILL.md`:

```bash
npx skills add payloadcms/skills
```

> [!WARNING]
> Use one delivery channel per project. Enabling both copies puts two skills named `payload` in scope and can produce conflicting guidance.
## What This Repo Is For

- Payload development workflows
- Contributor and maintainer tasks
- Repeatable PR, debugging, migration, and authoring flows
- Skills that are useful across agent ecosystems, not tied to a single model or editor

## Available Skills

### `payload`

> Legacy fallback providing comprehensive development guidelines for Payload projects whose installed package does not include a bundled skill.

**When to use:** Working with Payload projects (payload.config.ts, collections, fields, hooks, access control). Debugging validation errors, security issues, relationship queries, transactions, or hook behavior.

**Covers:**

- **Collections**: Auth, uploads, drafts, live preview configurations
- **Fields**: All field types including relationships, arrays, blocks, joins, virtual fields
- **Hooks**: beforeChange, afterChange, beforeValidate, field hooks
- **Access Control**: Collection, field, and global access patterns including RBAC and multi-tenant
- **Queries**: Local API, REST, and GraphQL with complex operators
- **Database Adapters**: MongoDB, Postgres, SQLite configurations and transactions
- **Advanced Features**: Jobs queue, custom endpoints, localization, plugins

[View full documentation →](skills/payload/README.md)

### `cms-migration`

> Interactive workflow to design Payload collections from source CMS data. Config-first approach: establish data structure through conversation before importing.

**When to use:** Migrating content to Payload from WordPress, Contentful, Strapi, Sanity, Webflow, or other CMSs. Working with data exports (JSON, CSV) that need to be mapped to Payload collections.

**Covers:**

- **Data Analysis**: Identify field types, relationships, and patterns from source data
- **Collection Design**: Generate Payload collection configs through iterative conversation
- **Field Mapping**: Complete reference for all Payload field types with source patterns
- **Migration Patterns**: WordPress, Contentful, Strapi field mappings
- **Common Pitfalls**: Select vs relationship disambiguation, rich text handling

[View full documentation →](skills/cms-migration/SKILL.md)

### `e2e-pr-assets`

> Contributor-focused workflow for attaching before/after admin UI evidence to Payload pull requests with GitHub-inline videos or screenshots.

**When to use:** Preparing or updating a Payload PR that needs reviewer-facing visual proof from e2e flows, especially when the fix is easiest to understand through before/after media in the PR body.

**Covers:**

- **Recording Plans**: Local `Before` / `After` shot lists with hidden PR-body comments
- **Video Evidence**: Record, convert, verify, and upload GitHub-inline H.264 MP4s
- **Screenshot Evidence**: Capture and attach before/after PNGs when screenshots are the right fit
- **Temporary Scenarios**: Agent-authored recording scripts for clearer demos than noisy committed tests
- **PR Body Updates**: Idempotent before/after sections with explicit incorrect/correct proof lines
- **Media Hygiene**: Startup-frame trimming, first-frame verification, and cleanup guidance

[View full documentation →](skills/e2e-pr-assets/README.md)

## Resources

- [Payload Documentation](https://payloadcms.com/docs)
- [Payload GitHub](https://github.com/payloadcms/payload)

## License

MIT

## WildGenie fork notes

- `skills/payload` holds the Payload 4 skill copied unchanged from `payload@4.0.0-beta.6` (`packages/payload/skills/payload`, tag v4.0.0-beta.6, commit 5ebbdebb). Upstream `main` still teaches Payload 3 APIs.
- Open upstream pull requests merged here: #8 (`codex/bundle-aware-skill`, prefer the version-matched bundled skill) and #6 (`codex/add-e2e-pr-assets-skill-main`, the `e2e-pr-assets` skill). Their branches are kept as `pr-8` and `pr-6`.
- `skills/cms-migration` is unchanged from upstream and still needs a Payload 4 review.
