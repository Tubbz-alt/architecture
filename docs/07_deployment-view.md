## 7. Deployment View

### 7.1 Test server [https://o2r.uni-muenster.de](https://o2r.uni-muenster.de)

[![deployment view test server](img/7.1-deployment-view-testserver.png)](img/7.1-deployment-view-testserver.png)

Motivation

:   The o2r infrastructure is driven by the research community's need for user friendly and transparent but also scalable and reliable solutions to increase computational reproducibility in the scientific publication process. To retrieve feedback from the community (public demo) and to increase software quality (controlled non-development environment), the current development state is regularly published on a test server.

Quality and/or Performance Features

:   The server is managed completely with [Ansible](https://www.ansible.com/) to ensure a well-document setup. The base operating system is CentOS Linux 7. The machine has 4 cores, 8 GB RAM, and a local storage ~100 GB, and runs on a VM host. The one machine in this deployment runs the full o2r reproducibility service, i.e. all microservices and a webserver to serve the user interfaces. It also runs the databases and ancillary services, such as a web traffic statistics service.

Mapping of Building Blocks to Infrastructure

:   All building blocks run in their own Docker container using an image provided via and build on [Docker Hub](https://hub.docker.com/r/o2rproject/) using a `Dockerfile` included in [each microservice's code repository](https://github.com/search?q=topic%3Amicroservice+org%3Ao2r-project+fork%3Atrue). The server is managed by the o2r team; external building blocks are managed by the respective organisation/provider.

### 7.2 Production (sketch)

[![deployment view test server](img/7.2-deployment-view-production-sketch.png)](img/7.2-deployment-view-production-sketch.png)

!!! Note
    This deployment view is a sketch for a potential productive deployment and intends to point out features of the chosen architecture and expected challenges or solutions.

Motivation

:   A productive system must be reliable and scalable providing a single reproducibility service API endpoint. It must also adopt the distribution and deployments to the hosted software and based on containers it naturally uses one of the powerful orchestration engines, such as [Docker Swarm](https://docs.docker.com/engine/swarm) or [Kubernetes](http://kubernetes.io/).

Quality and/or Performance Features

:   The services are redundantly provided via separated clusters of nodes for (a) running the reproducibility service's microservices and ancillary services, (b) running the document and search databases, (c) running ERC executions. The software in the data cluster can run in containers or bare metal. The clusters for app and compendia have access to a common shared file storage, a potential bottleneck. Performance of microservices can be easily scaled by adding nodes to the respective clusters.

Mapping of Building Blocks to Infrastructure

:   The o2r reproducibility services is managed by the o2r team similar to the test server. The other big building blocks, like publishing platforms or data repositories, are managed by the respective organisations.