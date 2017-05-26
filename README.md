# go4droid
To build an android app (with go bindings) in Docker

This Dockerfile was specifically written to build `golang.org/x/mobile/example/bind/android` (with [golang.org/x/mobile/cmd/gomobile](https://godoc.org/golang.org/x/mobile/cmd/gomobile)) but it should be possible to reuse or adapt it to build other android apps with go bindings (or even without).


## usage example:

	docker build -t go4droid .
	mkdir $HOME/.gradle # for caching
	go get -d golang.org/x/mobile/example/bind/...
	cd $GOPATH/src/golang.org/x/mobile/example/bind/android
	docker run --rm -v "$PWD":/home/gopher/project -v $HOME/.gradle:/home/gopher/.gradle -w /home/gopher/project --name go4droid -i -t go4droid /bin/bash
	gradle wrapper --gradle-version 2.10 # only needed once, to generate the gradle wrapper.
	./gradlew assembleDebug

