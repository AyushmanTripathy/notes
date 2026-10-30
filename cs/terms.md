Terms in CS
-----------

1. [Race Conditions](https://en.wikipedia.org/wiki/Race_condition)

## mTLS

- TLS but server verifies client certificate also.
- Used in microservices, kubernetes etc.

## SBOM

- Software bill of materials
- inventory listing of all packages, components, dependencies
- Helpful for
    1. Vulnerability managment
    2. Supply chain security
    3. License compliance

## SSE

- Server sent events
- Long lived HTTP connections opened from client side
- EventSource from browser to reconnect automatically
- Information is sent from server to client
- Ex. LLM Chats etc

## Webhooks

- Servers calling each other.
- One connection per calls 
- Servers can be inactive in between, no longed lived.

## Auto provisioning

- Creating/deleting infrastructure resource based on workload demand
- Triggered by "request to missing resource"
- Trigger Ex. A pod requests resources which no node pool can satisfy
- Ex. Karpenter, Azure Node Auto-Provisioning

## Auto Scaling

- Adjusts quantity or resource in response to load
- Ex. HPA in k8s, Azure VMSS

## Buffer nodes/Warm Pool

- preemptively provisioned nodes to avoid delay while scaling.
- Predictive scaling is something else, scaling before demand hits.

OS
--

1. Thrashing
    - caused by virtual memory
    - too much time is wasted for swaping memory
