# Is Docker still relevant?

Docker exploded under the scene a decade ago and brought containers into the mainstream, but some argue that docker's popularity may also lead to its downfall.

Does docker still matter?

## What does Docker do?

Docker has tree key components.

1.  Docker Client. This is the primary interface for interacting with Docker. It communicates with the docker daemon to manage various Docker objects, including images and containers.

2.  Docker Daemon. This is the core engine that manages container operations. It resides on the system running the docker software commonly known as the docker host. The docker daemon can utilize oci compliant run times like container D and cryo for running containers.

3.  Docker Registry. The most commonly used is docker hub. These registries store and distribute container images.

Before we move on, let's breifly touch on the open container initiative. OCI standized container runtime, image, and distribution specifications. This ensures that the container ecosystem remains open and not tied to a single vendor.

Now lets move on to key Docker commands.

- When you run `docker pull`, images download from registries.
- `docker build` uses a docker file to build an image. It adheres to the oci standards making it compatible across different run times.
- `docker run` starts a container from an image and is managed by the docker daemon. Here container D and cryo can serve as underlying run times.

In short, Docker has popularized several key concept in containerization:

1. a standard image format
2. streamline the building of container images
3. enabling the sharing of images through registries
4. facilitate the actual running of containers

While docker initially relied on proprietary technology, it has increasingly embraced Open Standards ike OCI. This openess has paved the way for alternative clients. runtimes and registries that also adhere to there standards. The vary stands and ecosystem Docker enabled may now be making the docker engine replaceable. WIth OCI standardizing container technology, and new tools delivering speed and efficiency, docker's unique value is questionable. Only time will tell if Docker can remain relevant, the whale may not be extinct yet, but its future is uncertain.
