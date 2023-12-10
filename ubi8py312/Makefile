TARGET:=python-3.12.1
ARCH:=$(shell uname -m)
OUTPUT:=$(TARGET)-1.el8.$(ARCH).rpm
build: $(OUTPUT)

$(OUTPUT): Dockerfile
	docker build --rm -t localhost/ubi8py312rpm .
	ID=$$(docker create localhost/ubi8py312rpm) \
	&& docker cp $$ID:/$(TARGET)-1.$(ARCH).rpm $(OUTPUT) \
	&& docker rm $$ID
