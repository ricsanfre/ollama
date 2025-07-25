
Run Ollama an Open WebUI with docker compose.


## Pre-requisites

-  Docker & docker-compose or Docker Desktop.
-  NVIDIA GPU — For GPU use, otherwise we’ll use the laptop’s CPU.
-  Python version 3
-  Disk space: The model files require at least 10GB of free space, but that is not enough. You should also have 20% of your total disk space available. Otherwise, you may encounter problems when starting Ollama, even if you have enough space for the model files.


## Instructions

1. **Clone this repository** (if you haven't already):

   ```bash
   git clone <your-repo-url>
   cd ollama
   ```

2. **Start the services**:

   ```bash
   docker compose up -d
   ```

   This will start both the Ollama backend and the Open WebUI frontend.

3. **Access the Web UI**:

   - Open your browser and go to: [http://localhost:3000](http://localhost:3000)

4. **Stopping the services**:

   ```bash
   docker compose down
   ```

### Using GPU for Inferencing

If you want to use GPU of your laptop for inferencing:

Update `docker-compose.yaml` file adding the 

```yaml
services:
  ollama:
    deploy:
      resources:
        reservations:
          devices:
            - driver: nvidia
              count: all
              capabilities: [gpu]
```


### Notes

- Ollama models are stored in the `./models` directory.
- Open WebUI data is stored in `./backend/data`.
- Both services are connected via the `genai-network` Docker network.

## Executing Ollam commands

-   List ollama models
    ```shell
    docker-compose exec -it ollama ollama list
    ```
-   Installing a new model
    ```shell
    docker-compose exec -it ollama ollama pull ${MODEL_NAME}
    ```

