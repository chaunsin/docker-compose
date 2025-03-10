export IMAGE_VERSION ?= latest
export IMAGE_NAME?=chaunsin/libreoffice-base:${IMAGE_VERSION}

logs:
	docker-compose -f docker-compose.yaml logs -f

start:
	docker-compose -f docker-compose.yaml up -d

stop:
	docker-compose -f docker-compose.yaml stop

# 注意会删除相关资源和数据
down:
	docker-compose -f docker-compose.yaml down

pull:
	docker-compose -f pull

# 构建镜像
build:
	DOCKER_BUILDKIT=1 docker build --progress=plain -t $(IMAGE_NAME) -f $(PWD)/Dockerfile $(PWD)

# 推送镜像
push:
	docker push $(IMAGE_NAME)