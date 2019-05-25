.env:
	@read -p "MYSQL_ROOT_PASSWORD: " MYSQL_ROOT_PASSWORD; \
	read -p "MYSQL_DATABASE: " MYSQL_DATABASE; \
	read -p "MYSQL_USER: " MYSQL_USER; \
	read -p "MYSQL_PASSWORD: " MYSQL_PASSWORD; \
	echo -e MYSQL_ROOT_PASSWORD=$$MYSQL_ROOT_PASSWORD >> .env; \
	echo -e MYSQL_DATABASE=$$MYSQL_DATABASE >> .env; \
	echo -e MYSQL_USER=$$MYSQL_USER >> .env; \
	echo -e MYSQL_PASSWORD=$$MYSQL_PASSWORD >> .env

stack: .env
	@read -p "Enter Stack Name: " stack; \
	source ./.env; \
	MYSQL_ROOT_PASSWORD=$$MYSQL_ROOT_PASSWORD \
	MYSQL_DATABASE=$$MYSQL_DATABASE \
	MYSQL_USER=$$MYSQL_USER \
	MYSQL_PASSWORD=$$MYSQL_PASSWORD \
	docker stack deploy --compose-file=docker-compose.yml $$stack

up: .env
	docker-compose up -d
