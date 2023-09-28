
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

token:
	docker exec -it elastic-elasticsearch-1 /usr/share/elasticsearch/bin/elasticsearch-create-enrollment-token -s kibana