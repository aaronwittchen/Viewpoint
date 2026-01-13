# Viewpoint

![CI](https://github.com/aaronwittchen/Viewpoint/actions/workflows/ci.yml/badge.svg)

A Vue 3 + Go web application with TypeScript support.

## Stack

- **Frontend**: Vue 3, TypeScript, Vite, Pinia
- **Backend**: Go, Gin
- **Build**: Bun (frontend), Go 1.23 (backend)

## Development

```bash
# Frontend
cd frontend && bun install && bun run dev

# Backend
cd backend && go run main.go
```

## Deployment

Built and deployed via Jenkins CI/CD to Kubernetes cluster.

- Images: `onionn/viewpoint-frontend`, `onionn/viewpoint-backend`
- URL: `https://viewpoint.k8s.local`
