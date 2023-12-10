TARGET:=python-3.11.7
ARCH:=$(shell uname -m)
OUTPUT:=$(TARGET)-1.el8.$(ARCH).rpm
build: $(OUTPUT)

$(OUTPUT): Dockerfile
	docker build --rm -t localhost/ubi8py311rpm .
	ID=$$(docker create localhost/ubi8py311rpm) \
	&& docker cp $$ID:/$(TARGET)-1.$(ARCH).rpm $(OUTPUT) \
	&& docker rm $$ID
