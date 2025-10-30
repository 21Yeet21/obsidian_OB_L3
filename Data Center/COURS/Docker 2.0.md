

## Docker Concepts

- Docker allows containerization of complex applications, offering flexibility and efficiency.
    
- Containers share the host OS kernel, making them lightweight and resource-efficient compared to virtual machines (VMs).
    
- Docker containers are portable, allowing creation locally, deployment in the cloud, and execution anywhere.
    
- Containers are loosely coupled, autonomous, and encapsulated, enabling updates or replacements without affecting others.
    
- Docker supports scaling and automatic replication of containers in data centers.
    
- Security is ensured through strict process isolation without requiring user configuration.
    

## Containers vs Virtual Machines

- Containers run natively on Linux, sharing the host kernel and executing as isolated processes.
    
- VMs run a complete guest OS via a hypervisor, incurring higher overhead beyond application logic resource use.
    

## Docker Architecture

- Docker Engine is a client-server application.
    
- Major components:
    
    - Docker daemon (dockerd) running as a long-lived server process.
        
    - REST API for programmatic interaction with the daemon.
        
    - Docker CLI client interface.
        
- Docker client communicates with the Docker daemon to build, pull images, run containers, etc.
    

## Docker Images and Containers

- A container is a running process isolated from the host and other containers.
    
- Containers use a private filesystem provided by a Docker image.
    
- Docker images include executables, runtime environment, dependencies, and filesystem objects needed to run an application.
    
- Images are layered; layers are read-only and represent filesystem differences.
    
- Containers add a writable layer on top of the image layers.
    
- Multiple containers can share the same image layer but have independent writable layers.
    
- Overlay filesystem manages layering with lowerdir (base), upperdir (writable), and merged (combined view).
    

## Docker Compose

- Workflow: create and test individual containers for each application component, then assemble into a complete application.
    
- Allows testing, sharing, and deployment of the full containerized application.
    

## Basic Docker Usage

- Common commands: `docker run`, `docker pull`, `docker stop`, `docker start`, `docker pause`, `docker exec`.
    
- Example: `docker run hello-world` pulls image if not local and runs a container sending output back to host.
    

## Dockerfile and Image Building

- Dockerfiles are scripts with instructions to build Docker images.
    
- Using Dockerfile helps manage changes as images grow complex.
    
- Docker build uses caching to reuse unchanged layers for efficiency.
    
- ARG and ENV directives manage build-time and runtime environment variables.
    
- Multi-stage builds allow separating build tools from final image to reduce image size.
    

## Storage: Volumes, Bind Mounts, TMPFS

- Docker supports persistent data storage via volumes, bind mounts, and tmpfs mounts.
    
- Volumes are preferred for persistence and managed by Docker independently of host filesystem specifics.
    
- Bind mounts link host directories/files to containers, performance-efficient but dependent on host directory structure.
    
- Tmpfs mounts store data in memory, suitable for temporary non-persistent data.
    

This summary covers the main Docker topics including concepts, architecture, image and container management, building images with Dockerfile, container lifecycle commands, storage options, and security/isolation principles. It should help you review key points for your exam preparation.Docker.pdf​
