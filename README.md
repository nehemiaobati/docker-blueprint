# Docker Blueprint

A standardized, portable, and self-contained structure for Docker projects.

## Project Structure
Every project must follow this structure to ensure portability:

```text
/docker/<project-name>/
├── docker-compose.yml       # The immutable source of truth
├── Dockerfile               # (Optional) Build context
├── .env.template            # Required vars (keys, paths)
├── Makefile                 # Standardized lifecycle commands
├── README.md                # Project-specific documentation
└── volumes/                 # Local mount points
    ├── data/
    └── config/
```

## Core Principles
1. **Absolute Self-Containment**: A project is 100% self-contained. All data—including configuration, databases, cache, and media/assets—must reside within the `volumes/` directory.
2. **Relative Paths**: No absolute paths are permitted in `docker-compose.yml`. All volume mounts must use relative paths (e.g., `./volumes/...`).
3. **Configuration**: Sensitive credentials must never be committed. Use `.env.template` to define required variables.
4. **Lifecycle Standardization**: Use the provided `Makefile` for unified management across all services.

## Lifecycle Management
- `make up`: Start the service in detached mode.
- `make down`: Stop and remove the service.
- `make logs`: Follow logs in real-time.
- `make backup`: Generate a compressed archive of the `volumes/` directory.
