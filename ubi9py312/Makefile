TARGET:=python-3.12.0
ARCH:=$(shell uname -m)
OUTPUT:=$(TARGET)-1.el9.$(ARCH).rpm
build: $(OUTPUT)

$(OUTPUT): Dockerfile
	docker build --rm -t localhost/ubi9py312rpm .
	ID=$$(docker create localhost/ubi9py312rpm) \
	&& docker cp $$ID:/$(TARGET)-1.$(ARCH).rpm $(OUTPUT) \
	&& docker rm $$ID
