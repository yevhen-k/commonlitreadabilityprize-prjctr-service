# Test Task for Prjctr (Web Service Part)

The goal of the project is to implement web-app wrapper for the trained deep learning NLP model. See the training repo: https://github.com/yevhen-k/commonlitreadabilityprize-prjctr

## Requirements
1. Docker
2. Docker-compose
3. [OPTIONAL] NVidia GPU with proprietary drivers
4. [OPTIONAL] nvidia-docker2

## Build

1. Clone the repo
2. Run
   ```bash
   docker-compose build
   docker-compose up
   ```

## Test as Separate Serices Locally
1. Clone the repo
2. Pull the Nginx container:
   ```bash
   sudo docker pull nginx:latest
3. Run nginx docker (use `-d` flag in production):
   ```bash
   sudo docker run --name nginx-proxy-container --rm -v `pwd`/nginx-local.conf:/etc/nginx/nginx.conf:ro --net=host nginx:latest
   ```
4. Build web application docker image:
    ```bash
    sudo docker build --tag web-dl-app .
    ```
5. Start web app container after nginx container:
    ```bash
    sudo docker run --rm -p 5000:5000 --gpus all web-dl-app
    ```
6. Check if it works locally:
    ```bash
    curl localhost
    curl -X POST localhost:80 -H 'Content-Type: application/json' -d '{"texts": ["hello, world", "this is a sentance"]}'
    ```

## References
1. Docker-compose functionality is inspired by [ishankhare.dev](https://ishankhare.dev/posts/1/)
