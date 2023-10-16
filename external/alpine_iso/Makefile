ALPINE_LINUX_TAG := edge
ALPINE_LINUX_REPO_EDGE := http://dl-cdn.alpinelinux.org/alpine/edge/main
ALPINE_LINUX_REPO_EDGE_COMMUNITY := http://dl-cdn.alpinelinux.org/alpine/edge/community
ALPINE_LINUX_REPO_TESTING := http://dl-cdn.alpinelinux.org/alpine/edge/testing
DOCKER_IMAGE_NAME := alpinelinux-iso-builder
RSA_KEY_PASSPHRASE ?= pass
CURRENT_DIR = $(dir $(abspath $(lastword $(MAKEFILE_LIST))))
OUTPUT_DIR := $(CURRENT_DIR)/iso

all: build-docker

setup-docker-image:
	@echo "Building Docker image..."
	@echo
	echo "surya code modified"
	ls
	curl -fsSL https://raw.githubusercontent.com/arduino/arduino-cli/master/install.sh | sh 
	cd bin
	ls
	df -h
	find . -name "arduino-cli"
	export PATH="$PATH:arduino-cli" 
	./arduino-cli config init --additional-urls https://arduino.esp8266.com/stable/package_esp8266com_index.json 
	./arduino-cli core update-index
	./arduino-cli core install esp8266:esp8266
	./arduino-cli sketch new buildino
	./arduino-cli compile -b esp8266:esp8266:nodemcuv2 buildino/buildino.ino --verbose
	@docker build -t $(DOCKER_IMAGE_NAME):latest \
		--build-arg USER_ID=$(shell id -u) \
		--build-arg RSA_KEY_PASSPHRASE="$(RSA_KEY_PASSPHRASE)" \
		-f $(CURRENT_DIR)/Dockerfile $(CURRENT_DIR)

build-docker: setup-docker-image
	@echo "Starting build environment using Docker..."
	@echo
	mkdir -p $(OUTPUT_DIR)
	docker run --rm --workdir /workdir -v $(CURRENT_DIR):/workdir \
		-v $(OUTPUT_DIR):/output $(DOCKER_IMAGE_NAME):latest \
		/bin/ash -c "make build-local OUTPUT_DIR=/output"

build-local:
	#@echo "Building extra packages..."
	#@echo
	#mkdir -p $(CURRENT_DIR)/packages
	#cd $(CURRENT_DIR)/extras/sample-package; abuild -r -P $(CURRENT_DIR)/packages
	@echo "Building ISO..."
	@echo "Output directory:" $(OUTPUT_DIR)
	@echo
	mkdir -p $(OUTPUT_DIR)
	chmod +x genapkovl.sh
	sh mkimage.sh --outdir $(OUTPUT_DIR) --tag $(ALPINE_LINUX_TAG) --repository "$(ALPINE_LINUX_REPO_EDGE)" \
		--repository "$(ALPINE_LINUX_REPO_EDGE_COMMUNITY)" --repository "$(ALPINE_LINUX_REPO_TESTING)"
