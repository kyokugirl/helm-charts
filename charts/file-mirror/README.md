# file-mirror

Helm chart for file mirroring using rsync

## Example

```yaml
# values.yaml
fullName: ubuntu-mirror
nginx:
  conf:
    serverName: "ubuntu.example.com"
rsync:
  source: "rsync://archive.ubuntu.com/ubuntu"
volume:
  hostPath: "/media/mirror/ubuntu" # customize as needed
```

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| fullName | string | "file-mirror" | Name of the application, mostly used as a prefix for resource names. |
| replicaCount | int | 2 | Number of replicas for the deployment. |
| nodeSelector | object | {} | Node selector for the Deployment pods. |
| nginx.tag | string | "stable-alpine" | Docker image tag for the nginx container. |
| nginx.conf.port | int | 80 | Port on which the nginx server will listen. |
| nginx.conf.serverName | string | "localhost" | Server name configuration for nginx. |
| rsync.tag | string | "alpine" | Docker image tag for the rsync container. |
| rsync.source | string | "" | Source location for rsync to mirror files from. |
| rsync.excludes | list | [] | List of patterns to exclude from rsync mirroring. |
| rsync.cronJob.schedule | string | "0 */2 * * *" | Cron schedule expression for the rsync job (default: every 2 hours). |
| rsync.cronJob.startingDeadlineSeconds | int | 60 | Deadline in seconds for starting the job if it misses its scheduled time. |
| volume.hostPath | string | "/tmp" | Host path to mount for storing mirrored files. |
| gateway.pathPrefix | string | "/" | Path prefix for the gateway configuration. |
| gateway.parentRefs | list | [] | List of gateway parent references for the HTTPRoute. Each item should contain name, namespace, and sectionName. |
| gateway.additionalRules | list | [] | Additional rules for the gateway configuration. |
