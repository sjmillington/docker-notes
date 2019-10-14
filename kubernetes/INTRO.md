## Kubernetes (K8s)

### What

`orchestatrator` - making many servers (or nodes) act like one. 

- A popular container orchestator created by google.
- It runs on top of docker, as a set of APIs in containers.
- Provides an API/CLI to manage containers across servers.
- Many clouds provide it for you.
- Many vendors make a 'distribution' of it.

### Why

- More Servers + A lot of change = Benefit of orchestration (S*C = O)
- If we don't have many servers or we're not redeploying a lot, checkout EBS or Heroku etc..
- Available as cloud or self-managed.
- 

## Kubernetes Vs Swarm

- Both container orchestrators running on top of Docker
- Both are solidly backed.
- Swarm is easier to deploy/manage.
- Kubernetes has more features and flexibility.
- Should know about both and compare each for specific use cases.

### Advantages to Swarm

- Ease
- Single vendor container solution (Docker)
- Runs wherever Docker runs
- Secure
- Easier to troubleshoot
- Generally better for small projects

### K8s

- Clouds will deploy/manage for you
- Wide adoption
- Flexible
- Trendy, will benefit your career (!)
