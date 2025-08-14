# private-llm
Easy to run docker setup for a private LLM with private Web Search and UI

- Web Search via SearXNG (StartPage as the only enabled engine)

## Instructions
1. Move dist.env into .env
2. Run 
    ```docker compose up```

## Optional: Enable integrated AMD GPU inference
1. To enable GPU inference, update `docker-compose.yml` with the following:


   ```yaml
    volumes:
      - /opt/rocm:/opt/rocm:ro # requires installing ROCm on your host
    devices:
      - /dev/kfd
      - /dev/dri
    environment:
      HSA_OVERRIDE_GFX_VERSION: "9.0.c" # depends on your GFX version
   ```

2. Set GPU memory usage to at least 1GB.

3. You should then see the GPU being detected:
   ```
   ollama      | time=2025-08-14T10:21:04.393Z level=INFO source=gpu.go:217 msg="looking for compatible GPUs"
   ollama      | time=2025-08-14T10:21:04.398Z level=INFO source=amd_linux.go:389 msg="skipping rocm gfx compatibility check" HSA_OVERRIDE_GFX_VERSION=9.0.c
   ollama      | time=2025-08-14T10:21:04.403Z level=INFO source=types.go:130 msg="inference compute" id=0 library=rocm variant="" compute=gfx90c driver=6.12 name=1002:1636 total="1.0 GiB" available="412.1 MiB"
   ```
