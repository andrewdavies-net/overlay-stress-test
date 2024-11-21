local build
go to build folder
podman build -t test2 -f Containerfile.copy

go to build container
podman build -t build-container -f Containerfile.overlay

run this container
podman run -it build-container

