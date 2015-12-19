# CHICKEN scheme in a Docker container running Alpine Linux

This is a Dockerfile that creates a image based on Alpine Linux
version 3.2 and installs Chicken version 4.10.0.

Alpine Linux is very small but has a package manager. It is based on
`musl` libc therefore we compile CHICKENscheme from source.

It is meant for developing purposes. After compiling your Scheme code
(with `-deploy` flag) you could copy all binaries and files from the
container and run it in a plain Alpine Linux based container. 

## Dockerfile

This image is created using the following Dockerfile:

	FROM alpine:3.2
	
	RUN apk update && apk add make gcc musl-dev 
	RUN wget -O - http://code.call-cc.org/releases/4.10.0/chicken-4.10.0.tar.gz | tar xz
	
	WORKDIR /chicken-4.10.0
	
	RUN make PLATFORM=linux && make PLATFORM=linux install
	
	RUN rm -fr /chicken-4.10.0 
	
	WORKDIR /
	
	CMD ["csi"]


## Resources

[CHICKENscheme](http://call-cc.org/)

[Alpine Linux](https://alpinelinux.org/)
