# Ubuntu 24.04 for Fly.io

This project runs:

```text
XFCE desktop through noVNC
Root terminal through ttyd
Nginx on port 8080
```

## Login

```text
Username: user
Password: 1234
```

The browser terminal opens as root after the ttyd login.

## Deploy

Install `flyctl`, sign in, and open this project folder.

Change the app name in:

```text
fly.toml
```

Replace:

```text
ubuntu24-flyio-change-me
```

with a globally unique Fly app name.

Then run:

```bash
fly launch --no-deploy
fly deploy
```

Fly uses the included Dockerfile and exposes internal port `8080`.

## Open the app

```bash
fly open
```

## Logs

```bash
fly logs
```

## Optional persistent storage

Create a volume in the same region as the Machine:

```bash
fly volumes create ubuntu_data --region ord --size 1
```

Then copy the mount section from:

```text
fly-volume.toml.example
```

into `fly.toml` and deploy again.

The volume mounts at:

```text
/data
```

Without a volume, files written to the Machine filesystem can disappear when the Machine is replaced.
