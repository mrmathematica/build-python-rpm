TARGET:=python-3.11.8
ARCH:=$(shell uname -m)
OUTPUT:=$(TARGET)-1.el9.$(ARCH).rpm
build: $(OUTPUT)

$(OUTPUT): Dockerfile
	docker build --rm -t localhost/ubi9py311rpm .
	ID=$$(docker create localhost/ubi9py311rpm) \
	&& docker cp $$ID:/$(TARGET)-1.$(ARCH).rpm $(OUTPUT) \
	&& docker rm $$ID
