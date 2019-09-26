BUILD_ID := $(shell git rev-parse --short HEAD 2>/dev/null || echo no-commit-id)
IMAGE_NAME := hashicorp/counting-service
VERSION := 0.0.2

BASEDIR := $(shell pwd)
APPNAME := $(shell basename `pwd`)

.DEFAULT_GOAL := help
help: ## List targets & descriptions
	@cat Makefile* | grep -E '^[a-zA-Z_-]+:.*?## .*$$' | sort | awk 'BEGIN {FS = ":.*?## "}; {printf "\033[36m%-30s\033[0m %s\n", $$1, $$2}'

build: ## Build docker image
	docker buildx build -t $(IMAGE_NAME):$(VERSION) . --build-arg APPNAME=$(APPNAME) --build-arg BASEDIR=$(BASEDIR) --platform linux/amd64
	docker tag $(IMAGE_NAME):$(VERSION) $(IMAGE_NAME):$(VERSION)

push: ## docker push the service images tagged 'latest' & 'BUILD_ID'
	docker push $(IMAGE_NAME):$(VERSION)

run: ## run docker image locally
	docker run -it $(IMAGE_NAME):$(VERSION)
