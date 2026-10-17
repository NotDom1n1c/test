# test

website where you learn how to code

A static website served by non-root nginx, created with [LAUNCHPAD](https://github.com/notdom1n1c/launchpad).

| | |
|---|---|
| Live (local cluster) | http://test.localhost |
| Pipeline | `.github/workflows/launchpad.yml` |
| Kubernetes manifests | `deploy/` (Argo CD watches this folder) |

## How a change goes live

1. Edit `index.html` / `style.css` and push to `main`.
2. GitHub Actions tests it, builds the image, smoke-tests the container and scans it with Trivy.
3. The image goes to `ghcr.io/notdom1n1c/test` and the pipeline writes the new tag into `deploy/kustomization.yaml`.
4. Argo CD sees the commit and rolls out the new version.

The pipeline commits to `main` after every deploy, so run `git pull` before your next push.
