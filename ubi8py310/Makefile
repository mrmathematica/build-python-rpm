TARGET:=python-3.10.13
ARCH:=$(shell uname -m)
OUTPUT:=$(TARGET)-1.el8.$(ARCH).rpm
build: $(OUTPUT)

$(OUTPUT): Dockerfile
	docker build --rm -t localhost/ubi8py310rpm .
	ID=$$(docker create localhost/ubi8py310rpm) \
	&& docker cp $$ID:/$(TARGET)-1.$(ARCH).rpm $(OUTPUT) \
	&& docker rm $$ID
