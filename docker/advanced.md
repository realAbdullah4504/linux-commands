# Docker Advanced Topics

## Health Checks

### Docker Health Check
```dockerfile
HEALTHCHECK --interval=30s --timeout=5s --start-period=10s --retries=3 \
  CMD curl -f http://localhost:3000/health || exit 1
```

## Docker Build

### Multi-Stage Builds
Multi-stage Docker builds help create smaller, more efficient images by separating build-time dependencies from runtime dependencies.

### Docker BuildKit
Enhanced build system with improved performance and features.

Resources:
- https://docs.docker.com/build/buildkit/

## Docker Scout
Security scanning tool for Docker images and containers.

## Immutable Infrastructure
Consistent environments across all stages (development, staging, production) using Docker containers.

## System Information

### Docker System Commands
```bash
# Display container storage information
docker system df

# Monitor container resource usage
docker stats
```

## Best Practices

### Container Security
- Use minimal base images
- Run containers as non-root users
- Regularly update base images
- Scan images for vulnerabilities

### Performance Optimization
- Use multi-stage builds
- Optimize layer caching
- Remove unnecessary dependencies
- Use .dockerignore files

### Production Deployment
- Use docker-compose for orchestration
- Implement health checks
- Set up proper logging
- Monitor container performance
