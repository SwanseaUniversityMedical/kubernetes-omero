# Changelog

## 2026-06-25 — Chart version 0.4.15

### Version updates

- **busybox** (omero-server init container): `1.37` → `1.38.0`
- **Redis Helm dependency** (omero-web): `17.3.11` → `27.0.12`
- **CloudNativePG** (CI test): `1.28.1` → `1.29.1`

### Chart metadata

- Both `omero-server` and `omero-web` `Chart.yaml` upgraded from `apiVersion: v1` to `apiVersion: v2` (Helm 3 standard).
- Added `type: application` to both `Chart.yaml` files.
- `omero-web` dependencies moved into `Chart.yaml` (required by `apiVersion: v2`); `requirements.yaml` kept in sync for reference.

### Removed workarounds

- Removed `bitnamilegacy/redis` image override from `omero-web/values.yaml` (was a temporary workaround for [#55](https://github.com/manics/kubernetes-omero/issues/55)). The Bitnami Redis chart 27 uses standard `docker.io/bitnami/redis` images which do not require authentication.

### Known issues / follow-up

- The K3s v1.21 entry in the CI test matrix (`.github/workflows/test_and_publish.yml`) targets an EOL Kubernetes release and could be removed.
- The `annotations:` block in `omero-server/templates/ingress.yaml` may produce malformed YAML when `websockets.encrypted=true` and user-supplied `ingress.annotations` are both set; a `merge`-based approach would be cleaner.
