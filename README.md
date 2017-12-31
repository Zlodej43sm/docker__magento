# Docker for Magento

Docker setup environment for Magento.

## Magento 1.x & 2.x

### Add project settings:

1. Download you project files into - **www/**

2. Set you mounted services - **docker-compose.yml**

3. Set virtual hosts for container - **config/vhost**

4. Set credentials for remote repositories - **config/auth.json**

5. **ONLY Magento 2.x**. Set sync folder path - **docker-sync.yml**


### Docker init project:

1. Create project environment image (tag name same as in  **docker-compose.yml**).

```bash
docker image build -t you_group/project_name:latest path_to_docker_file
```

2. **ONLY Magento 2.x**. Create & launch sync image.

```bash
docker-sync start
```

3. Launch project containers via **docker-compose**.

```bash
docker-compose up -d
```

4. Add project host name to local hosts on your laptop **sudo vi /etc/hosts**

### Commands

1. **docker ps** - show all launched services/containers 

2. **docker-compose start/stop/restart/pause/unpause**

3. **docker-sync start/stop/sync**

4. **docker exec -it you_service/container_name bash** - execute launched service/container by name

5. **docker inspect you_service/container_name** - get launched service/container full info
