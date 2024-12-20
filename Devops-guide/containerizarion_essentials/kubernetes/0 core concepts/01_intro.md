# Introduction

Kubernetes is an open source orchestrator for deploying containerized applications

- developed by Google
- introduced in 2014
- proven infrastructure for distributed systems of all scales
- now maintained by Cloud Native Computing Foundation (CNCF)

## Development velocity

- velocity is not defined in terms of simply raw speed
- It is rather the number of features that can be shipped maintaining the availability of the software
- Core concepts of kubernetes that help in this area are:

  - **Immutability**
    - It means once an artifact is created in the system, it does not change via user modifications
    - With a mutable system, the current state of the infrastructure is not represented as a single artifact, but rather as an accumulation of incremental updates and changes over time
    - In contrast, in an immutable system, rather than a series of incremental updates and changes, an entirely new, complete image is built, where the update simply replaces the entire image with the newer image in a single operation
    - > It is possible to imperatively change running containers, but this is an antipattern to be used only in extreme cases where there are no other options (e.g., if it is the only way to temporarily repair a mission-critical production system). And even then, the changes must also be recorded through a declarative configuration update at some later time, after the fire is out

  - **Declarative configuration**
    - In K8s, everything is a *declarative configuration object*
    - *Declarative configuration* is a way to describe the desired state of the system, rather than the steps to get there (which is called as *imperative configuration*)
    - With an imperative approach, the configuration would say “run A, run B, and run C.” The corresponding declarative configuration would be “replicas equals three
    - The idea of storing declarative configuration in source control is often referred to as `infrastructure as code`

  - **Self-healing**
    - K8s is an online, self-healing system
    - After receiving a declarative configuration, K8s will continuously work to ensure that the actual state of the system matches the desired state
    - K8s will not only initialize the system, but also continuously monitor it, and if it detects any divergence from the desired state, it will automatically correct it
    - > Online self-healing systems improve developer velocity because the time and energy you might otherwise have spent on operations and maintenance can instead be spent on developing and testing new features.

  - **Shared reusable libraries and tools**

## Scaling (of both software and teams)

- As products grow, it's inevitable that the team size will grow as well and the software will need to scale
- k8s achieves it by favouring *decoupled architecture*
- **Decoupled Architecture**
  - In a decoupled architecture, each component is separated from other components by defined APIs and service load balancers
  - APIs provide a buffer between implementer and consumer
  - load balancers provide a buffer between running instances of each service
  - Decoupling servers via APIs makes it easier to scale the development teams because each team can focus on a single, smaller microservice with a comprehensible surface area
- **Scaling for Applications**
  - Immutable, declarative nature of k8s makes this scaling trivial to implement
  - K8s can scale applications horizontally by adding more instances of the same service
  - It can also scale vertically by increasing the resources available to a single instance of a service
- **Scaling for Clusters**
  - One of the challenges of scaling machine resources is predicting their use
  - K8s achieves this by abstracting the infrastructure as each node is similar to the other
  - K8s can scale the number of nodes in the cluster
- **Scaling for Teams**
  - As projects grow, the number of teams working on them will also grow which demands a microservice architecture
  - To address this, there has been a development of decoupled, service-oriented teams that each build a single microservice
  - Kubernetes provides numerous abstractions and APIs that make it easier to build these decoupled microservice architectures:
    - *Pods*, or groups of containers, can group together container images developed by different teams into a single deployable unit
    - Kubernetes *services* provide load balancing, naming, and discovery to isolate one microservice from another
    - *Namespaces* provide isolation and access control, so that each microservice can control the degree to which other services interact with it
    - *Ingress* objects provide an easy-to-use frontend that can combine multiple microservices into a single externalized API surface area
- **Separation of concerns**
  - The application developer relies on the service-level agreement (SLA) delivered by the container orchestration API, without worrying about the details of how this SLA is achieved
  - Likewise, the container orchestration API reliability engineer focuses on delivering the orchestration API’s SLA without worrying about the applications that are running on top of it
  - This enables to scale infrastructure operations to manage many machines with a single small, focused team

## Abstracting your infrastructure

- **Public Cloud Challenges**: Public cloud APIs often focus on infrastructure elements like virtual machines rather than application-centric concepts, making it difficult for developers to manage applications across multiple environments
- **Kubernetes as a Solution**: Adopting Kubernetes allows developers to work with application-oriented container APIs, which decouples them from specific machines and enhances scalability and portability across different cloud infrastructures
- **Easy Environment Transfers**: With Kubernetes, transferring applications between environments becomes straightforward, as developers can simply send declarative configurations to new clusters, facilitating hybrid deployments
- **Infrastructure Abstraction**: Kubernetes provides plug-ins that abstract away cloud-specific services, enabling the creation of load balancers and managing storage across various public and private infrastructures, thus increasing flexibility

## Efficiency

- Efficiency can be measured by the ratio of the useful work performed by a machine or process to the total amount of energy spent doing so
- Running a server incurs costs related to power, cooling, space, and compute power, making it essential for system administrators to manage utilization effectively; Kubernetes helps automate application distribution across clusters, optimizing resource usage and reducing waste
- Kubernetes enhances efficiency by allowing developers to quickly and inexpensively create test environments as containers within a shared cluster using namespaces, enabling multiple developers to utilize fewer machines and thereby maximizing resource usage and reducing costs
- Using a small number of containers for deployments instead of multiple virtual machines significantly reduces costs and enhances development velocity by providing reliable feedback and detailed insights for quickly identifying code issues

## Cloud native ecosystem

- **Extensibility and Community Support**: Kubernetes is designed to be extensible, fostering a vibrant and welcoming community that actively contributes to its ongoing development and improvement.
- **Rich Ecosystem of Tools**: The widespread adoption of Kubernetes has resulted in a robust ecosystem of open-source tools and services, enabling developers to leverage existing solutions and accelerate their projects.
- **Diverse Solutions for Various Needs**: A wide array of tools for tasks such as machine learning, continuous development, and serverless programming are available within the Kubernetes ecosystem, providing developers with numerous options to enhance their workflows.
- **Empowered Decision-Making**: With many high-quality solutions available, developers can choose the best tools tailored to their specific requirements, empowering them to optimize their development processes
- **Focus on Core Innovation**: By utilizing community-supported projects within the cloud-native ecosystem, developers can concentrate on building their unique business logic and services, driving innovation and value for their organizations
- **Complexity of Solutions**: The open-source ecosystem presents challenges due to the variety of available solutions and often a lack of end-to-end integration
- **Role of CNCF**: The Cloud Native Computing Foundation (CNCF) provides technical guidance and serves as a neutral home for cloud-native projects, helping users navigate the ecosystem
- **Project Maturity Levels**: CNCF categorizes projects into three maturity levels: sandbox (early development, not recommended for general use), incubating (proven utility and stability but still growing), and graduated (fully mature and widely adopted)
- **Focus on Adoption**: While there are many sandbox projects, only a few incubating and graduated projects exist, with Kubernetes being one of the few fully graduated projects, indicating its maturity and reliability
- **Guided Adoption**: Understanding these maturity levels helps organizations make informed decisions about adopting cloud-native projects based on their stability and community support
