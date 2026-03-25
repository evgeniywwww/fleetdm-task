# FleetDM Helm Deployment

Helm chart for running FleetDM plus MySQL (StatefulSet) and Redis (Helm dependency) on a local Kubernetes cluster.

## Prerequisites

- Minikube
- kubectl
- Helm (v3+)
- make

## Run locally

From the `fleetdm/` directory:

```bash
make cluster
make deps
make install
```

## Access

```bash
make port-forward
```

Open `http://localhost:8080`.

## Verification

```bash
kubectl get pods -n default
```

You should see pods for:
- FleetDM (`Deployment` `fleetdm-fleet`)
- MySQL (`StatefulSet` `fleetdm-mysql`)
- Redis (from the `redis` chart dependency)

Logs:

```bash
make logs
```

## Database initialization

A Helm hook `Job` runs `fleet prepare db` after install/upgrade (`post-install,post-upgrade`).
It waits for MySQL by polling the MySQL service port with `nc -z`.

## Uninstall

```bash
make uninstall
```

## Notes

- MySQL has no persistence (no PVC).
- Access is via port-forward (no Ingress in this chart).
- MySQL password comes from `.Values.mysql.password` (defaults to `"fleet"` if empty).