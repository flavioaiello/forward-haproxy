
[![Docker Pulls](https://img.shields.io/docker/pulls/flavioaiello/forward-haproxy.svg)](https://hub.docker.com/r/flavioaiello/forward-haproxy/)
[![Docker Automation](
https://img.shields.io/docker/automated/flavioaiello/forward-haproxy.svg)](https://hub.docker.com/r/flavioaiello/forward-haproxy/)

# Forward-Haproxy
This general-purpose proxy forwards any request based on the resolver defined by the `RESOLVER` environment variable and runs completely without further configuration.

## Use-Cases

### Ingress
This forward proxy can be used inbound scenarioss (ingress) where split horizon name servers are supported. In this case, the DNS entries in the local scope must be specified so that the request can be forwarded locally.

### Egress
This forward proxy can be used in outbound scenarios (egress) where split horizon name servers are supported. In this case, the DNS entries in the global scope must be specified so that the request can be forwarded outbound.

### Legacy
This forward proxy can also be used in legacy scenarios for load balancing whithin traditional workloads.

## Supported modes
- HTTP forward based on HTTP Host-Header.
- TCP forward based on TLS Server-Name-Indication (SNI). (TLS offloading is not supported)

## Testing
Local testing can be performed simply by providing the test recipe:
```
docker stack deploy -c apps.yml apps
```

Now the endpoints below should be reachable:
- http://app1.localtest.me
- http://app2.localtest.me

## Performance
Haproxy offeres outstanding performance based on zero-copy and tcp-splicing.
