PROJECT ?= sandbox-rabbitmq-cluster-federation
ENV     ?= .env

DC ?= docker compose --project-name=$(PROJECT) --env-file=$(ENV)


## help: print this message
.PHONY: help
help: Makefile
	@echo
	@echo 'Usage: make <TARGETS> ... <OPTIONS>'
	@echo
	@sed -n 's/^##//p' $< | column -t -s ':' | sed -e 's/^/ /'
	@echo
	@echo 'By default print this message.'
	@echo


$(ENV):
	@echo "ERROR: $(ENV) file not found!" >&2
	@exit 1


## deploy: build and deploy
.PHONY: deploy
deploy: $(ENV)
	@echo '---> [$@]'
	$(DC) up --build --detach --remove-orphans


## remove: stop and remove current project
.PHONY: remove
remove: $(ENV)
	@echo '---> [$@]'
	$(DC) rm --force --stop --volumes


## cleanup: remove none images
.PHONY: cleanup
cleanup:
	@echo '---> [$@]'
	docker images | grep none | xargs docker rmi
