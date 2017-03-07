# Developer notes

## Build
### Locally

To build the docker image locally, run the following command

```bash
docker build -t scw1109/jet-gatling:local .
```

### CI

This project uses [Dockerhub](https://hub.docker.com) as the build system as well as the docker repository.
Visit [here](https://hub.docker.com/r/scw1109/jet-gatling/) to see more details.

#### Setup notes

Dockerhub could link to Github and automatically build a Github repository with a Dockerfile.

Activate the service integration on Github side to allow Dockerhub receive notification whenever a push or other events.

Also, there are some configuration on the Dockerhub setup pages. Added a tag build to build whenever a tag is created, this is useful for release.

## Release

### Release steps

1. Before start, make sure the build status of Dockerhub is success for the master branch.
1. To create a new release, follow the [instructions](https://github.com/blog/1547-release-your-software) to create a Github release.
   * Dockerhub will use the Github tag name as the docker image tag.
   Hence, it should follow the naming convention like ```0.3```.
   * For Github "release title", convention is something like ```v0.3```.     
1. Dockerhub will then build a new release and publish.
