
SHELL = /bin/bash
NAME = cl-captcha-bot
CONTAINER = fgd-captcha-bot
DOCKERFILE = Dockerfile


.PHONY: build force test debug

build:
	docker build -f "${DOCKERFILE}" -t "${NAME}" .

force:
	docker build -f "${DOCKERFILE}" -t "${NAME}" --no-cache .

rebuild:
	docker stop $(CONTAINER)
	docker rm $(CONTAINER)
	date > build_date
	docker build -f "${DOCKERFILE}" -t "${NAME}" .

test:
	$(MAKE)
	docker run -it $(NAME):latest

debug:	test
	docker run -it --user=root --entrypoint ${SHELL} $(NAME):latest

start:
	docker run -d --name $(CONTAINER) --env-file ./env.txt --restart always $(NAME)
	
stop:
	docker stop $(CONTAINER)
	docker rm $(CONTAINER)
	
logs:
	docker logs $(CONTAINER)
