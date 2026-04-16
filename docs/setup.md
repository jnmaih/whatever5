# Setup and CI/CD workflow

1. Run Backstage locally and open the software templates page.
2. Select **Demo NGINX CNCF NBG CI/CD Template**.
3. Fill in fields:
   - Name: `demo-nginx-cncf-nbg` (or your component name)
   - Owner: `user:guest` or your own user/group entity reference
   - Classpath: `com.example.demo.nginx` (or your preferred namespace)
   - Repository Location: `https://github.com/<your-org>/<your-repo>`
4. Run the template. It will:
   - create your repo content in GitHub
   - push to `main`
   - register the component in the Backstage catalog
   - render TechDocs with creator metadata derived from the signed-in Backstage user

## GitHub Actions

Pipeline file: `.github/workflows/ci.yaml`

- runs on push/PR to main
- runs a placeholder lint job
- runs a TechDocs build verification job

## Backstage validation

1. Open created component in Backstage via catalog.
2. Go to **Docs** tab -> TechDocs content is rendered from this repository (`docs/`).
3. Go to **CI/CD** tab -> after plugin setup, status can show GitHub Actions checks.

## Optional entity annotation for GitHub Actions plugin

Update the component metadata with:

```yaml
metadata:
   name: "<component-name>"
  annotations:
    github.com/project-slug: "<your-org>/<your-repo>"
spec:
   owner: "<owner-entity-ref>"
```

And add the `backstage.io/techdocs-ref` annotation if missing:

```yaml
    backstage.io/techdocs-ref: "dir: ."
```
