# stable-diffusion-louso-docker-cuda
SD AUTOMATIC 1111 install docker

Prepare the directory mapping in your host (Создаём директории):
```
mkdir -p /MY-DATA-DIR && cd /MY-DATA-DIR
mkdir models outputs
sudo chown 10000:$UID -R models outputs
sudo chmod 775 -R models outputs
```
# With the latest CUDA version
```
docker run -it --name sdw --gpus all --network host \
  -v $(pwd)/models:/app/stable-diffusion-webui/models \
  -v $(pwd)/outputs:/app/stable-diffusion-webui/outputs \
  --rm siutin/stable-diffusion-webui-docker:latest-cuda \
  bash webui.sh --share
```
# Nvidia CUDA image
```
nvidia-docker buildx build -f Dockerfile.cuda \
                           --platform linux/amd64 \
                           --build-arg BUILD_DATE=$(date -u +'%Y-%m-%dT%H:%M:%SZ') \
                           --build-arg BUILD_VERSION=custom-cuda \
                           -t siutin/stable-diffusion-webui-docker:custom-cuda .
```


# Check your current CUDA vrsion
```
nvidia-smi -x -q |sed -n 's/.*<cuda_version>\(.*\)<\/cuda_version>.*/\1/p'
```
# Проверка версии CUDA
```
nvidia-smi -x -q |sed -n 's/.*<cuda_version>\(.*\)<\/cuda_version>.*/\1/p'
```
