# Resilience Patterns

## Chaos Engineering

- Intensionally inject failures (kill instances, add latency) to verify resilience
- Ex. Netflix's Chaos Monkey

## Patterns

### Timeout

- Give up on a operation instead of waiting forever
- Duration is calculated using p95/p99
- Idempotency is required.

### Circuit Breaker

- Sits infront of a service (db, api etc)
- it bypasses the service and a fallback response is sent.
    - if service starts failing too often or too slowly
    - prevents calls from hanging or failing one by one
- Can be in following states, Open, Closed, Half-Open
- After cooldown, few requests are used to test before service is Opened
- This is a resilience pattern, preventing cascading failure

### Retry

- Instead of propagating error, callers waits and tries again
- Exponential backoff, meaning progressively longer periods
- Jitter, Randomness in time to avoid synchorized bursts.
- Constraints needed
    - Only idempotent requests
    - All error types need not be retried ex. 404, 400
    - Maximum retry count

### Bulkhead

- Isolates elements into pools, so failure doesnot consume all resources.
- Prevents "resource exhaustion cascading failure".
- Implementations
    1. Thread pool isolation
    2. Semaphore isolation
    3. Connection pool partitioning
    4. Process/container-level isolation

### Rate Limiting / Throttling

- Enforcing a quota per client, regardless of whether system is struggling.
- Response is 429, with `Retry-After` header.
- Active when system is healthy
- Prevents single client hogging capacity

### Load Shedding

- Dropping some request when system is under stress
- Prevent total collapse like out-of-memory
- Response is 503 or 429
- Rate limiting is preventing overload, this is surviving overload.

### Graceful Degradation

- Continue with reduced funtionality rather than failing.
- Identify core vs non core functionality
- Its better to fail first in non-critical paths
- Ex. "Render product page without product page", "Show posts without like count"

## Deployment Strategies

### Canary release

- Rolling out the new version to small subset of users
- Risk mitigation is the goal
- Often split randomly

### Blue-Green release

- We maintain 2 enviroments, but only one serves the traffic.
    1. Blue is serving 100%, Green is idle
    2. New version entirely goes to Green
    3. Once Green is tested, router switches to Green
    4. If something goes wrong, switch back to Blue instantly
- Challange become how to deal with db schema changes.
- Rollback speed is instant

### A/B Testing

- Measuring impact of change to certain user groups
- Comparison and experiment is the goal
- For business & data science
