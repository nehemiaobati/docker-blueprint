# Docker Blueprint Standard

This repository establishes a rigid, portable standard for all Docker projects on this system.

## The Regulation
1. **Isolation**: No global dependencies. Every service must define its networks and volumes relative to its own folder.
2. **Persistence**: All data MUST be mounted to the local `volumes/` directory relative to the `docker-compose.yml`. No absolute paths.
3. **Configuration**: Credentials and secrets are never committed. Only `.env.template` exists in the repo.
4. **Lifecycle**: Deployment is handled via `Makefile` targets:
   - `make up` = `docker compose up -d`
   - `make logs` = `docker compose logs -f`
   - `make backup` = Generates a tarball of the `volumes/` directory.

## Project Structure
```text
/docker/<project-name>/
├── docker-compose.yml       # Immutable source of truth
├── .env.template            # Required vars (keys, paths)
├── Makefile                 # Lifecycle commands
├── README.md                # Project-specific docs
└── volumes/                 # Local persistence
    ├── data/
    └── config/
```
