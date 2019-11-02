---
title: servicemesh.es
---

# Service Mesh Comparison

## What is a Service Mesh?

A Service Mesh is a dedicated infrastructure layer that adds features to connections between services. It allows to control traffic and gain insights throughout the system. Observability, Traffic Shifting (for Canary Releasing), Resiliency features such as Circuit Breaking and Retry/Timeout and automatic mutual TLS can be configured once and enforced in a decentralized fashion. In contrast to libraries, which are used for simiar functionality, a Service Mesh does not require any code changes. Instead, it adds a layer of additional containers that implement the features reliably and agnostic to technology or programming language.  

## Who needs a Service Mesh?

The value of a Service Mesh grows with the number of services an application consists of. Logically, Microservices-Architectures are the most common applicaton for a Service Mesh. But apart from the plain number of services, their specific interaction might be even more important to if a Service Mesh can improve the control, reliability, security and observability of the services. Even a monolith could benfit from a Service Mesh and some concrete Microservice-Applications might not.

## Service Mesh Implementations

-  **Istio** 
  If you have heard about Service Mesh, you have probably heard about Istio too. Istio is by far the most popular Service Mesh, because it has the most features and it is backed by Google and IBM.
-  **Linkerd 2**
   While Istio made the Service Mesh popular, Linkerd was the first Service Mesh and quite successful. Still the developers decided to build a new version - Linkerd 2 - committed to usability, performance and Kubernetes as the underlying platform.  
-  **AWS App Mesh**
   Not long after Service Mesh became a thing, AWS added their own Service Mesh for Applications on AWS.
-  **Consul/Consul Connect**
   Consul is well known as a Service Discovery Solution. They decided to implement the Service Mesh pattern into their architecture to provide even more advanced features. 
-  **maesh**
   As the name already reveals, maesh is the Service Mesh based on Traefik, a cloud native API gateway.
-  **Kuma**
   Similiar to maesh, Kuma is also a very new Service Mesh made by developers of an API Gateway - Kong.

**Service Mesh Interface**
In the face of the vast variety of Service Mesh implementations, a group of companies, including Microsoft, Buoyant (developying Linkerd) and Consul, joined forces to create a common standard for Service Mesh features. The result, the Service Mesh Interface specification, means to enable tools based on Service Mesh Features (such as Flagger for Canary Releasing automation) to be compatible with any Service Mesh rather than binding to a specific set of implementations. Service Mesh users also benefit from the ability to change their Service Mesh implementation without changing the configuration.

  

## How to decide for a Service Mesh Implementation

The list above shows that Service Mesh



## Technical Comparison 

|                                                              | ![istio-blue-logo](img/istio.png)          | ![linkerd](img/linkerd.png)                                  | ![awsappmesh](img/awsappmesh.png)  | ![consul](img/consul.png)                        | ![maesh](img/maesh.svg) | ![kuma](img/kuma.png)   |
| ------------------------------------------------------------ | ------------------------------------------ | ------------------------------------------------------------ | ---------------------------------- | ------------------------------------------------ | ----------------------- | ----------------------- |
|                                                              | **Istio**                                  | **Linkerd 2**                                                | **AWS App Mesh**                   | **Consul**                                       | **mæsh**                | **Kuma**                |
| Current version                                              | 1.3                                        | 2.6                                                          |                                    | 1.6                                              | 0.7                     | 0.2                     |
| License                                                      | Apache License 2.0                         | Apache License 2.0                                           | Closed Source                      | Mozilla License                                  | Apache License 2.0      | Apache License 2.0      |
| Developed by                                                 | Google, IBM, Lyft                          | Buoyant                                                      | Amazon                             | HashiCorp                                        | containous              | Kong                    |
| Service Proxy                                                | Envoy                                      | [linkerd-proxy](https://github.com/linkerd/linkerd2-proxy)   | Envoy                              | defaults to Envoy, exchangeable                  | Traefik                 | Envoy                   |
| Platform                                                     | Kubernetes, Consul & Nomad                 | Kubernetes                                                   | Kubernetes, ECS, Fargate, EKS, EC2 | Kubernetes, Nomad, standalone                    | Kubernetes              | Kubernetes, "universal" |
| Automatic Sidecar Injection                                  | yes                                        | yes                                                          | yes                                | yes                                              | yes (per Node)          | yes                     |
| **Supported Protocols**                                      | ---                                        | ---                                                          | ---                                | ---                                              | ---                     | ---                     |
| TCP                                                          | yes                                        | yes                                                          | yes                                | yes                                              | yes                     | yes                     |
| HTTP/1.1+                                                    | yes                                        | yes                                                          | yes                                | yes                                              | yes                     | yes                     |
| HTTP/2                                                       | yes                                        | yes                                                          | in preview                         | yes                                              |                         |                         |
| gRPC                                                         | yes                                        | yes                                                          | in preview                         | yes                                              |                         |                         |
| **[Service Mesh Interface](https://smi-spec.io/) compatibility** | ---                                        | ---                                                          | ---                                | ---                                              | ---                     | ---                     |
| [Traffic Access Control](https://github.com/deislabs/smi-spec/blob/master/traffic-access-control.md) | yes                                        | no                                                           | no                                 | yes                                              | yes                     | no                      |
| [Traffic Specs](https://github.com/deislabs/smi-spec/blob/master/traffic-specs.md) | yes                                        | no                                                           | no                                 | no                                               | yes                     | no                      |
| [Traffic Split](https://github.com/deislabs/smi-spec/blob/master/traffic-split.md) | yes                                        | yes                                                          | no                                 | no                                               | yes                     | no                      |
| [Traffic Metrics](https://github.com/deislabs/smi-spec/blob/master/traffic-metrics.md) | yes                                        | yes                                                          | no                                 | no                                               | no                      | no                      |
| **Monitoring Features**                                      | ---                                        | ---                                                          | ---                                | ---                                              | ---                     | ---                     |
| Access Log Generation                                        | yes                                        | no ( [tap](https://linkerd.io/2/reference/cli/tap/)-Feature instead) | yes                                | yes                                              | yes                     | yes                     |
| "[Golden Signal](https://landing.google.com/sre/sre-book/chapters/monitoring-distributed-systems/#xref_monitoring_golden-signals)" Metrics Generation | yes                                        | yes                                                          | yes                                | yes, depending on the Proxy used                 | yes                     | no*                     |
| Integrated, pre-configured Prometheus                        | yes                                        | yes                                                          | no                                 | no                                               | yes                     | no                      |
| Integrated, pre-configured Grafana                           | yes                                        | yes                                                          | no                                 | no                                               |                         | no                      |
| Per-Route Metrics                                            | no                                         | yes                                                          |                                    | depending on the Proxy used                      |                         | no                      |
| Dashboard                                                    | yes, [Kiali](https://www.kiali.io)         | yes                                                          | yes, AWS Cloud Watch               | yes, showing only configuration and availability | no                      | no                      |
| Compatible Tracing-Backends                                  | Jaeger, Zipkin, Solarwinds                 | all Backends supporting [OpenCensus](https://opencensus.io/service/exporters/) | AWS X-Ray                          | Datadog, Jaeger, OpenTracing, Honeycomb, Zipkin  | Jaeger                  | -                       |
| **Routing Features**                                         | ---                                        | ---                                                          | ---                                | ---                                              | ---                     | ---                     |
| Load Balancing                                               | yes (Round Robin, Random, Least Connction) | [yes (EWMA](https://linkerd.io/2/features/load-balancing/) exponentially weighted moving average) | yes                                | yes                                              | yes                     |                         |
| Percentage-based Traffic Splits                              | yes                                        | yes                                                          | yes                                | yes                                              | yes                     | yes                     |
| Header- and Path-based Traffic Splits                        | yes                                        | no                                                           | yes                                | yes                                              | no                      | no*                     |
| **Resilience Features**                                      | ---                                        | ---                                                          | ---                                | ---                                              | ---                     | ---                     |
| Circuit Breaking                                             | yes                                        | no                                                           | no                                 | no*                                              | yes                     | no*                     |
| Retry & Timeout                                              | yes                                        | yes                                                          | yes                                | Timeout yes, Retry no*                           | yes                     | no*                     |
| Fault Injection                                              | yes                                        | yes, [by adding a Deployment and a traffic split config](https://linkerd.io/2/tasks/fault-injection/) |                                    | no*                                              | no                      | no*                     |
| Delay Injection                                              | yes                                        | no                                                           |                                    | no*                                              | no                      | no*                     |
| **Security Features**                                        | ---                                        | ---                                                          | ---                                | ---                                              | ---                     | ---                     |
| mTLS                                                         | yes                                        | [yes, not for TCP](https://linkerd.io/2/features/automatic-mtls/) |                                    | yes, via [Vault](https://www.vaultproject.io)    | no                      | yes                     |
| Authorization Rules                                          | yes                                        | no                                                           |                                    | yes                                              | no                      | yes                     |

*= might be possible through manual configuration/templating of proxy



### Resources, Latency and Usability