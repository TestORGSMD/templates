# Dokploy Templates

External template registry for [Dokploy](https://github.com/dokploy/dokploy).

## Structure

```
templates/
  index.json              # canonical list of all templates
  <template-id>/
    docker-compose.yml    # the compose file served on deploy
    logo.png              # template logo (referenced in index.json)
```

## Template schema (`index.json`)

Each entry in `index.json` must follow this shape:

```json
{
  "id": "my-app",
  "name": "My App",
  "version": "1.0.0",
  "description": "Short description (max 150 chars).",
  "logo": "https://raw.githubusercontent.com/dokploy/templates/main/templates/my-app/logo.png",
  "links": {
    "github": "https://github.com/org/repo",
    "website": "https://example.com",
    "docs": "https://docs.example.com"
  },
  "tags": ["tag1", "tag2"]
}
```

| Field | Required | Notes |
|-------|----------|-------|
| `id` | ✅ | Unique slug, matches directory name |
| `name` | ✅ | Display name |
| `version` | ✅ | Current version string |
| `description` | ✅ | Max 150 characters |
| `logo` | ✅ | Absolute URL to logo image |
| `links.github` | ✅ | |
| `links.website` | ❌ | |
| `links.docs` | ❌ | |
| `tags` | ✅ | Array of lowercase strings |

## Adding a template

1. Create `templates/<id>/` directory
2. Add `docker-compose.yml`
3. Add a logo image (`logo.png`, `.svg`, etc.)
4. Add an entry to `templates/index.json`
5. Open a PR — no app redeploy needed, changes are live within 5 minutes (cache TTL)

## Versioning

The `main` branch is what Dokploy fetches by default. To pin to a specific version,
set `TEMPLATES_REPO_URL` in your backend `.env`:

```env
TEMPLATES_REPO_URL=https://raw.githubusercontent.com/dokploy/templates/v2
```
