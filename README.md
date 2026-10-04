# compose-preview-imports generated output

This repository stores the generated output of
[compose-preview-imports](https://github.com/yschimke/compose-preview-imports): one
`design-artifacts/<slug>` delivery branch per imported project, and the catalog registry document
that tells a preview server which of them to serve. Imports, workflows and documentation live in
the source repository.

Nothing here is edited by hand.

| Path | Written by |
| --- | --- |
| `design-artifacts/<slug>` branches | `import.yml`'s `publish` job in the source repository, after each import build. |
| [`.compose-preview/catalogs.json`](.compose-preview/catalogs.json) on `main` | `catalog-registry.yml` in the source repository, regenerated from its `imports/` directory whenever an import lands. |

A preview server serves these catalogs by nominating this repository as a catalog registry:

```
--catalog-registry yschimke/compose-preview-imports-out
```

(`SERVE_CATALOG_REGISTRY=yschimke/compose-preview-imports-out` in the prebuilt image.) The server
reads `.compose-preview/catalogs.json` from this repository's default branch and serves each listed
catalog from this repository's own `design-artifacts/<system>` branch.

The delivery branches are build output from third-party projects — see the source repository's
[`docs/SECURITY.md`](https://github.com/yschimke/compose-preview-imports/blob/main/docs/SECURITY.md)
for what that means and what it does not. Do not protect them: they are force-pushed by machine.
