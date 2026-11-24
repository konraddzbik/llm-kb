
Run ollama alongside tih openwebui
```bash
docker run -d -p 3000:8080 \
-v ollama:/root/.ollama \
-v open-webui:/app/backend/data \
--name open-webui \
--restart always ghcr.io/open-webui/open-webui:ollama
```

run only open web ui, and ollama already installed 
```bash
docker run -d -p 3000:8080 \
--add-host=host.docker.internal:host-gateway \
-v open-webui:/app/backend/data \
--name open-webui \
--restart always ghcr.io/open-webui/open-webui:main
```