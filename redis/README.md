# Clear Linux* OS `redis` container image

<!-- Required -->
## What is this image?

`clearlinux/redis` is a Docker image with `redis` running on top of the
[official clearlinux base image](https://hub.docker.com/_/clearlinux). 

<!-- application introduction -->
> [Redis](https://redis.io/) is an open source (BSD licensed), in-memory data structure 
> store, used as a database, cache and message broker. It supports data structures such 
> as strings, hashes, lists, sets, sorted sets with range queries, bitmaps, hyperloglogs, 
> geospatial indexes with radius queries and streams. 

For other Clear Linux* OS
based container images, see: https://hub.docker.com/u/clearlinux

## Why use a clearlinux based image?

<!-- CL introduction -->
> [Clear Linux* OS](https://clearlinux.org/) is an open source, rolling release
> Linux distribution optimized for performance and security, from the Cloud to
> the Edge, designed for customization, and manageability.

Clear Linux* OS based container images use:
* Optimized libraries that are compiled with latest compiler versions and
  flags.
* Software packages that follow upstream source closely and update frequently.
* An aggressive security model and best practices for CVE patching.
* A multi-staged build approach to keep a reduced container image size.
* The same container syntax as the official images to make getting started
  easy. 

To learn more about Clear Linux* OS, visit: https://clearlinux.org.

<!-- Required -->
## Deployment:

### Deploy with Docker
The easiest way to get started with this image is by simply pulling it from
Docker Hub. 

*Note: This container uses the same syntax as the [official redis
image](https://hub.docker.com/_/redis).


1. Pull the image from Docker Hub: 
    ```
    docker pull clearlinux/redis
    ```

2. Start a container using the examples below:
   ```
   docker run --name some-redis --network some-network -d clearlinux/redis redis-server --protected-mode no
   ```
   
3. connecting via redis-cli
   ```
   docker run -it --network some-network --rm clearlinux/redis redis-cli -h some-redis
   ```

<!-- Optional -->
### Deploy with Kubernetes

This image can also be deployed on a Kubernetes cluster, such as [minikube](https://kubernetes.io/docs/setup/learning-environment/minikube/).The following example YAML files are provided in the repository as reference for Kubernetes deployment:

- [`redis-deployment.yaml`](https://github.com/clearlinux/dockerfiles/blob/master/redis/redis-deployment.yaml): example using default configuration to create a basic redis service.
- [`redis-deployment-conf.yaml`](https://github.com/clearlinux/dockerfiles/blob/master/redis/redis-deployment-conf.yaml): example using your own custom configuration to create a redis service.



Steps to deploy redis on a Kubernetes cluster:

1. If you want to deploy `redis-deployment.yaml` 

   ```
   kubectl create -f redis-deployment.yaml
   ```

   Or if you want to deploy `redis-deployment-conf.yaml`

   ```
   kubectl create -f redis-deployment-conf.yaml
   ```

2. Install redis bundle and connect to the service, where 30001 is the port number defined in your service.

   ```
   swupd bundle-add redis-native
   redis-cli -h <nodeIP> -p 30001
   ```

<!-- Required -->
## Build and modify:

The Dockerfiles for all Clear Linux* OS based container images are available at
https://github.com/clearlinux/dockerfiles. These can be used to build and
modify the container images.

1. Clone the clearlinux/dockerfiles repository.
    ```
    git clone https://github.com/clearlinux/dockerfiles.git
    ```

2. Change to the directory of the application:
    ```
    cd redis/
    ```

3. Build the container image:
    ```
    docker build -t clearlinux/redis .
    ```

   Refer to the Docker documentation for [default build arguments](https://docs.docker.com/engine/reference/builder/#arg).
   Additionally:
   
   - `swupd_args` - specifies arguments to pass to the Clear Linux* OS software
     manager. See the [swupd man pages](https://github.com/clearlinux/swupd-client/blob/master/docs/swupd.1.rst#options)
     for more information.

<!-- Required -->
## Licenses

All licenses for the Clear Linux* Project and distributed software can be found
at https://clearlinux.org/terms-and-policies
