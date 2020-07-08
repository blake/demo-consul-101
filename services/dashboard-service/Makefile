BUILD_ID := $(shell git rev-parse --short HEAD 2>/dev/null || echo no-commit-id)
IMAGE_NAME := hashicorp/dashboard-service
VERSION := 0.0.4

.DEFAULT_GOAL := help
help: ## List targets & descriptions
	@cat Makefile* | grep -E '^[a-zA-Z_-]+:.*?## .*$$' | sort | awk 'BEGIN {FS = ":.*?## "}; {printf "\033[36m%-30s\033[0m %s\n", $$1, $$2}'

build: ## Build docker image
	docker build -t $(IMAGE_NAME):$(VERSION) .
	docker tag $(IMAGE_NAME):$(VERSION) $(IMAGE_NAME):$(VERSION)

multi-arch:
	docker buildx build --tag '$(IMAGE_NAME):$(VERSION)' --platform linux/386,linux/amd64,linux/arm64 --output="type=registry" .

push: ## docker push the service images
	docker push $(IMAGE_NAME):$(VERSION)

run: ## run docker image locally
	docker run -it $(IMAGE_NAME):$(VERSION)
