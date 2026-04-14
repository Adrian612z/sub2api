# Athena Fork Workflow

This fork uses a two-branch model:

- `main`: upstream mirror reference branch from `Wei-Shaw/sub2api`
- `athena-prod`: AthenaAPI production maintenance branch

## Daily Rules

1. Make Athena-specific changes on `athena-prod`.
2. Tag releases from `athena-prod` using `v*` tags.
3. Deploy production with pinned GHCR tags, never `latest`.

## Sync Upstream

```bash
git fetch upstream
git checkout athena-prod
git merge upstream/main
```

If conflicts appear, resolve them on `athena-prod`, test locally, then push.

## Release

```bash
git checkout athena-prod
git pull origin athena-prod
git tag v0.1.111-athena.1
git push origin athena-prod --tags
```

The existing release workflow in this fork publishes GHCR images. Repository variable `SIMPLE_RELEASE=true` is enabled so releases only build the x86_64 GHCR image by default.

## Production Deployment

Production deployment config lives in the separate private repository `Adrian612z/athenaapi-deploy`.
Use a pinned image such as:

```text
ghcr.io/adrian612z/sub2api:v0.1.111-athena.1
```

Do not deploy `weishaw/sub2api:latest` directly in production.
