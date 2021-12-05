
SHELL = /bin/bash
NAME = cl-captcha-bot
CONTAINER = fgd-captcha-bot
DOCKERFILE = Dockerfile
SRC_DIR = `pwd`/../sources

.PHONY: build force test debug

build:
	docker build -f "${DOCKERFILE}" -t "${NAME}" .

force:
	docker build -f "${DOCKERFILE}" -t "${NAME}" --no-cache .

dev:
	docker build --target builderdeps -f "${DOCKERFILE}" -t "${NAME}-dev" .
	docker run  --env-file ./env.txt --mount type=bind,source="${SRC_DIR}",target=/srv/app --entrypoint "/srv/app/entrypoint.sh" -it "${NAME}-dev"

remove:
	docker stop $(CONTAINER)
	docker rm $(CONTAINER)
	docker image rm $(NAME)

stop:
	docker stop $(CONTAINER)

start:
	docker start $(CONTAINER)

test:
	$(MAKE)
	docker run -it $(NAME):latest

debug:	test
	docker run -it --user=root --entrypoint ${SHELL} $(NAME):latest

create:
	docker run -d --name $(CONTAINER) --env-file ./env.txt --restart always $(NAME)
	
delete:
	docker stop $(CONTAINER)
	docker rm $(CONTAINER)
	
logs:
	docker logs $(CONTAINER)
