TARGET:=python-3.11.3
ARCH:=$(shell uname -m)
OUTPUT:=$(TARGET)-1.el7.$(ARCH).rpm
build: $(OUTPUT)

$(OUTPUT): Dockerfile
	docker build --rm -t localhost/ubi7py311rpm .
	ID=$$(docker create localhost/ubi7py311rpm) \
	&& docker cp $$ID:/$(TARGET)-1.$(ARCH).rpm $(OUTPUT) \
	&& docker rm $$ID
