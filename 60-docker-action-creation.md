# 60 - Docker Action Creation

Docker actions allow you to package your action logic and dependencies in a container.

## Key Features
- **Environment Isolation:** Guaranteed to run in the exact same environment every time.
- **Complexity:** Best for actions that require many dependencies or a specific OS (Linux only).

## Structure (`action.yml`)
```yaml
name: 'Docker Hello World'
description: 'Greet someone'
inputs:
  who-to-greet:
    description: 'Who to greet'
    required: true
    default: 'World'
runs:
  using: 'docker'
  image: 'Dockerfile'
  args:
    - ${{ inputs.who-to-greet }}
```

## `Dockerfile`
```dockerfile
FROM alpine:3.10
COPY entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
```

## Exam Tips
- Docker actions only run on Linux runners.
- They are generally slower than composite or JavaScript actions because of the overhead of building/pulling the image.
- Use `runs.image: 'docker://node:18'` to use a pre-built image from a registry.
