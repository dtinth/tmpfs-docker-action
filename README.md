# tmpfs-docker-action

A GitHub Action that configures Docker to use tmpfs for improved build performance.

## Usage

```yaml
- name: Setup Docker with tmpfs
  uses: dtinth/tmpfs-docker-action@main
  with:
    size: '4G'  # Optional, defaults to 4G
```

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `size` | Size of the tmpfs mount (e.g., 4G, 8G) | No | `4G` |

## Outputs

| Output | Description |
|--------|-------------|
| `docker-root-dir` | The Docker root directory path |

## Example

```yaml
name: Build with tmpfs
on: [push]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Setup Docker with tmpfs
        uses: dtinth/tmpfs-docker-action@main
        with:
          size: '8G'
      
      - name: Build Docker image
        run: docker build -t my-app .
```

## How it works

This action:
1. Stops the Docker service
2. Creates a tmpfs mount at `/tmp/docker`
3. Configures Docker to use the tmpfs as its data root
4. Restarts Docker and waits for it to be ready
5. Outputs the Docker root directory and tmpfs information

This can significantly improve Docker build performance, especially for builds with many layers or large intermediate files, by using RAM instead of disk storage.