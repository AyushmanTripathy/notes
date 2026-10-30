# Kubernetes

From [Azure](https://azure.microsoft.com/en-us/solutions/kubernetes-on-azure/get-started)

## Components and concepts

### Cluster

- cluster of virtual or on premises machines
- Machines are called `nodes`
- These nodes share compute, network, storage resources
- Each cluster has a master node, rest are worker nodes
- Worker nodes are responsible for running pods

### Pod

- Smallest deployable unit
- containerized applications or workloads are called pods
- Pods can contain multiple containers
- All containers in one pod have the same network, volumes, start/stop together
- Hence container working closly, pattern is called `sidecar`
- Pods have only one IP, hence containers can talk using localhost

```
Kubernetes manages Pods
Pods contain Containers
Containers run Applications
```

#### Pod Lifecycle

Pod's status.phase can be one of the following,
- `Pending`: image pulling, allocation resources etc
- `Running`: Bound to node & all containers created
    - At least one container is running/starting/restarting
    - Includes `CrashLoopBackOff` or `Terminating`
- `Succeeded`: All containers terminated successfully & won't be restarted
- `Failed`: All containers terminated and atlest one failed.
- `Unknow`: Pod's state couldn't be obtained (ex. communicaiton error)

NOTE: CrashLoopBackOff are not phase, but only display value

Container states are as follows
- `Waiting`: Not running or terminated, kubectl shows a `Reason`, ex. pulling image
- `Running`: already running.
- `Terminated`: The container either failed or succedeed

Restart policy `spec.restartPolicy` is Pod level
- Can be `Always`, `OnFailure`, `Never`
- Sidecar have container level policy as Always
- Deployment create using Always. Jobs use OnFailure or Never

NOTE: Restarting container is not same as restarting pod.

#### Pod Termination

1. kubectl trigger the pod deletion
2. kube-apiserver records the terminating info.
    - Pod status becomes Terminating
3. kubelet notices Terminating state and starts shutdown.
4. `preStop` is executed if grace period is non zero.

Force deletion can cause hanging process on the node.

### Control Plane

- Kubernetes maintains a number of objects that form control plane
- Developers and operators interact with cluster through master node using `kubectl`
- Commands issued to master node are received by `kube-apiserver` the talks with `kube-controller-manager`
- kube-controller-manager is responsible for handling worker node operations
- Commands issued to worker node are received by `kubelet`

### Deploying

- Master node maintains current state & configurations in `etcd`
- etcd is a key value database
- We describe a new desired state to cluster in form of a YAML file
- kube-controller-manager takes this yaml file and tasks it to `kube-scheduler`
- kube-scheduler decides what pods to start, issues commands to kubelets
- In a deployment, the desired state becomes the current state
- Kubernetes supports rollbacks, rolling updates and pausing rollouts
- Deployments use ReplicaSets with identically configured pods running, hence kubernetes becomes self healing.
- Each worker also contains a `kube-proxy`, ensure network traffic reaches correct pod

### Controllers

- Continuously watches the cluster ensures reality matches desired state
- For example, no of pods running
- there are many of these
    - Deployment controller
    - ReplicaSet controller
    - DaemonSet controller

### Service

- The problem,
    - Pods are temporary
    - Applications cannot depend on changing IP addresses
- Services receive a stable IP and DNS names ex. `database.default`
- Service sits between clients and Pods
- This performs L4 (Transport) LB, handled by kube-proxy
- Simpler like round-robin/random etc.

#### Ports

3 ports can be specified
1. port: Port exposed by the service
2. targetPort: Port on Pod/container to which traffic is forwarded to
3. nodePort: Allows traffic from NodeIP:nodePort, must be unique in for a node.

Container level specification
1. containerPort: which port it expects to receive traffic on
2. hostPort: Port on the node to be allocated to container.

### Ingress

- Exposes HTTP or HTTPs routes from outside the cluster to Services.
- To expose other than HTTP, service needs to be used.
- Along with Ingres resource, we need an Ingress Controller.
- Can we used to direct traffic using rules
- Supports TLS termination
    - Meaning traffic to subsequent Services are plaintext
    - Needs Secret

### Namespaces

- Logical partitions inside a kubernetes cluster

```
Kubernetes Cluster
├── Namespace: dev
│ ├── Pods
│ ├── Services
│ └── Deployments
│
├── Namespace: test
│ ├── Pods
│ ├── Services
│ └── Deployments
│
└── Namespace: prod
  ├── Pods
  ├── Services
  └── Deployments
```

- Same resource name exist in different namespaces ex. `dev/app` or `prod/app`
- Pods are isolated automatically
- Access can be given to specific namespaces
- Quota limits and policies can be applied at namespace level

### Secrets

- Kubernetes has native secrets that are stored in `etcd`
- That can be set using kubectl and Pod can use it by yaml.

```
Developer
    │
    ▼
Kubernetes Secret
    │
    ▼
API Server
    │
    ▼
etcd
    │
    ▼
Kubelet
    │
    ▼
Pod
```

- This leads to secrets being shared to many components
- The prefered way is to use services like key vault
    1. Pod requests secret
    2. CSI driver authenticates with Key Vault
    3. Secret is fetched
    4. Secret is mounted as a file inside pod at `/mnt/secrets`
- Pod proves Managed identity or workload identity, no passwords required 
- By using key vault, we can rotate passwords without rebuiling images.

```
┌────────────┐
│ Azure Key  │
│   Vault    │
└─────┬──────┘
      │
      ▼
┌──────────────────┐
│ CSI Driver       │
│ AKS Add-on       │
└─────┬────────────┘
      │
      ▼
┌─────────────┐
│ Pod         │
│ /mnt/secrets│
└─────────────┘
```

### Rollouts

- Process of updating an application or serivce gradually without downtime
    1. Incremental updates
    2. Zero downtime
    3. Revision tracking, every time deployment is changed, new version is created

### ReplicaSet

- Workload controller which maintains a stable, guaranteed number of identical Pods.
- Ensures high avalibility.
- Its self healing mechanism.
- its works using a `reconciliation loop`, comparing actual number to desired number
- Three pillars
    1. Replicas, number stating no of identical Pod instances
    2. Selector, label matching to identify which Pods the ReplicaSet is managing
    3. Pod template, blueprint used to build and launch new Pods.
- The ReplicaSet controller work under controller-manager in control plane.
- Typically ReplicaSets are created through Deployments.

#### Rolling Updates in Deployment

- RollingUpdate is the default deployment strategy
- deployment is trigger when a Pod template changes, 
- Working
    1. New ReplicaSet is created
    2. old ReplicaSet is scaled down while new is scaled up
    3. Eventually we have only new ReplicaSet

```
strategy:
  type: RollingUpdate
  rollingUpdate:
    maxUnavailable: 1
    maxSurge: 1
```

- Contraints can be added to this scaling
    - `maxUnavailable`: how many pods can be unavalible during update
    - `maxSurge`: how many additional pods can exist during update
- this can be numbers or percentages, unavaliable are rounded down and surge is rounded up
- Defaults are 25% for both

- strategy can also be `Recreate`, which produces downtime
    1. all old Pods are terminated
    2. new Pods are created

##### Progress Deadline secounds

- `minReadySecounds`: how long a new pod need to remain ready before its considered available
- `progressDeadlineSeconds`: how long to wait for a deployment to make progres, before reporting stalled
- It is required that minReadySecounds < progressDeadlineSecounds

### StatefulSets

- Needed when Pods need a persistent identity
- `ordinal` refers to a number that identifies the position of a Pod
- Difference from deployment
    - Deployment treats Pods as interchangeable replicas
    - StatefulSets give each Pod a persistant identity
    - Identity consists of ordinal, stable network identity, stable storage

### DaemonSet

- For Pods that provide node-local facilites
- For running "some Pods on every worker node"

### cert-manager

- `cert-manager` performs ACME for kubernetes
- Operates as in-cluster controller, as standard Pods on your worker nodes
- Still considered a part of control plane.

### Probes

- `probe` are health checks done by kubelet periodically on containers
- Probes are of 3 types
    1. `Startup`: Has the application started?
        - Allow other probes to run
        - Runs only once
    2. `Liveness`: Is application still alive?
        - Failure tells kubelet to restart the container
        - Runs periodically
    3. `Readiness`: Can this container accepts traffic?
        - Failure removes from Service endpoints
        - Ex. db has failed, ie restarting container maynot help
        - Runs periodically

- Without Liveness probe k8s still uses restartPolicy when ever container stops
- Use when container can be running but unhealthy

### PodDisruptionBudget

- Keeps atlest a min number of Pods alive at all time.
- Limits the number of Pods of replicated app that can be down simultaneously.
- Works for `voluntary disruptions` i.e. caused by human or controller
- `Involuntary` would mean things out of our control, power failure etc

### HorizontalPodAutoscaler

- Deploys more Pods in response to increase in load.
- Runs in interval of horizontal-pod-autoscaler-sync-period, defaults to 15s.
- Scaling is done through `scale` interface in deployments or StatefulSets
- For a Rollout, it sets the desired replica count not the ReplicaSets
- Rollout controller then splits the count into ReplicaSets

### Eviction

#### Node pressure Eviction

- kublet proactively terminates Pods to reclaim resources on nodes
- No respect for PDB or terminationGracePeriodSeconds
- Eviction can be soft or hard,
    1. `evictionSoft`: breached threshold is tolerated for `evictionSoftGracePeriod`
        - respects for eviction-max-pod-grace-period
    2. `evictionHard`: instantly after breach of threshold
        - No respect for eviction-max-pod-grace-period
- Following proccess is followed,
    1. preStop
    2. SIGTERM to pid 1
    3. Grace period, upto eviction-max-pod-grace-period is allowed (hard -> 0)
    4. SIGKILL
- Pod selection is based on
    1. Whether pod's resource usage exceeds requests
    2. Pod Priority
    3. pod's resource usage relative to request

#### API Initiated Eviction

- Following proccess is followed,
    1. preStop 
    2. SIGTERM
    3. Grace period, gets terminationGracePeriodSeconds
    4. SIGKILL
- Grace period count down starts from preStop, not from SIGTERM
- In parrallel, Pod is removed from EndpointSlice, stops receiving requests.
- respects grace period & PDB
- Used by VPA, not HPA

### Service Accounts

- Nonhuman identity represented as Kubernetes API object
- It provides authentication, not authorization

## External Components

Below components are not native feature of kubernetes,

### Service Mesh

- Infrastructure layer that manages communication between services
- Service mesh pulls all this implimentation from application
- For microservices, each serivce needs
    1. Service discovery
    2. Load balancing
    3. Retries & timeouts
    4. Traffic control (A/B testing, canary releases)
    5. Encryption
    6. Observability
- Generally done through a `sidecar` pattern
    1. Lightweight proxy is deployed alongside each service instance
    2. Network traffic flows through this sidecar proxy
    3. Proxies form the `data plane`
    4. Separate `control plane` configures these proxies
- Examples Istio, Linkerd, Consul connect

#### Istio

- Kubernetes already provides (Service) but its L4
    1. Service discovery
    2. Traffic distribution
- Istio provides L7 capabilities
    1. Routing based on HTTP headers
    2. Retry logic on endpoints
    3. Only a certain namespace can call an service
    4. Divide traffic in percentages
    5. For performing mTLS, (Mutual TLS, server also verifies client's certificate) 
- Bypasses kube-proxy's load balancing, but uses Service for discovery.

### Helm

- Its a package manager for kubernetes
- Instead of many yaml files for using kubectl
- We can create an helm chart, that can be reused.

```sh
# Updating image of deployment

kubectl set image deployment/mortgage-ai-backend backend=acr.azurecr.io/mortgage-ai-backend@sha256:abc123

helm upgrade mortgage-ai-backend ./chart --set image.digest=sha256:abc123
```

### Agro Rollouts

- Agro is Kubernetes controller + CRDs.
- It extends basic deployment funtionality
- It introduces `Rollout` resource, which extends deployment.

#### Rollout

- A `scaleDownDelaySeconds` can be set for delay before ReplicaSet scale down.
- Default value is 30s
- `scaleDownDelayRevisionLimit` caps how many old ReplicaSets can stay scaled up while they wait out scaleDownDelaySeconds
- Setting this to 0, means not scaleDownDelaySecounds

### VerticalPodAutoscaler

- Upates the requests and limit dynamically based on demand.
- Its an CRD, Unlike HPA
- Can be Recreate, InPlaceOrRemote or InPlace.
- Uses the Eviction API if Recreate is required.
