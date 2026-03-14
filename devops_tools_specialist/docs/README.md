# DevOps Tools Specialist Reference

## Primary SOP
`/home/ubuntu/TinyHive-sops/development/devops_tools_sop.md`

## Core Knowledge Domains

### Docker Quick Reference
```bash
# Images
docker build -t name:tag .
docker pull image:tag
docker images

# Containers
docker run -d -p 8080:80 image
docker ps -a
docker stop container
docker rm container

# Volumes
docker volume create name
docker volume ls
```

### Dockerfile Best Practices
```dockerfile
# Multi-stage build
FROM node:18 AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

FROM nginx:alpine
COPY --from=builder /app/dist /usr/share/nginx/html
```

### GitHub Actions Workflow
```yaml
name: CI
on: [push, pull_request]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
      - run: npm ci
      - run: npm test
```

### Git Branching Strategies
| Strategy | Use Case |
|----------|----------|
| GitHub Flow | Simple, continuous deployment |
| Git Flow | Release-based, multiple environments |
| Trunk-Based | High-frequency merges, feature flags |

### Build Tools Comparison
| Tool | Best For |
|------|----------|
| Webpack | Complex apps, full control |
| Vite | Fast dev, modern projects |
| Rollup | Libraries, ES modules |
| esbuild | Speed-critical builds |

### CI/CD Pipeline Stages
1. **Build** - Compile, bundle, Docker build
2. **Test** - Unit, integration, E2E
3. **Security** - SAST, dependency scan
4. **Deploy** - Staging, production
5. **Verify** - Smoke tests, monitoring

## Related Consultants
- `gitlab_engineering_architect` - Architecture
- `chaos_engineer` - Resilience testing
- `monitoring_engineer` - Observability
