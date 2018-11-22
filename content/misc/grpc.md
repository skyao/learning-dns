---
date: 2018-11-22T14:50:00+08:00
title: Grpc
weight: 9902
menu:
  main:
    parent: "misc"
description : "grpc dns 方案"
---

https://github.com/bigcommerce/grpc-proposal/blob/master/A2-service-configs-in-dns.md 

看来google也是把service config encode在dns里的



https://github.com/grpc/grpc/blob/master/doc/naming.md 

grpc可以有自己的resolving plugin

grpc service :k8 service的想法原来早就有人想了:

https://groups.google.com/forum/#!topic/grpc-io/DkweyrWEXxU/discussion 

For additional background, I also created an issue for TXT record support in Kubernetes' kube-dns, citing gRPC as an use case: https://github.com/kubernetes/dns/issues/38

My idea is that there would be a 1:1 mapping between a Kubernetes service and a gRPC service, something that developers seem to like. For example, you'd point clients to mysvc.myns.svc.mycluster.example.com (or a shorter relative name). That's a DNS hostname managed by kube-dns. With the new support, it would return the appropriate TXT record. More in detail:

There's a controller (daemon) in the Kubernetes cluster in charge of pushing gRPC config changes. It sends an update request on the mysvc service object. kube-dns, also running in the cluster, sees the object change and starts serving new TXT records. So far, gRPC itself doesn't need to be involved, i.e. there's no special protocol between servers and clients (or grpclb). Clients keep using DNS.

With your current design, the controller pushes a config with e.g. a 1% canary. Accurate percentages is not even the main issue; determinism and proper health check tracking are. Assuming that exactly 1% of clients pick up the change, now you have the issue of figuring if a replica that just crashed did it because of the new config or for unrelated reasons. Engineers really hate it when a configuration change gets rolled back automatically because of a random external event. Conversely, when an unhealthy service is seeing an elevated crash rate and you try to push a new config to stop the bleeding, it's very valuable to know if the new settings are making instances stable again. 

In both cases, you need to track which configuration each client is using. You could do this through e.g. monitoring (each client reports the current config version) and correlate that with health checks.

Or, more simply, you could have the controller pick up N victims, push a config with a field along the lines of

`"hosts": "host1:port,host2:port,..."`

wait n=TTL seconds and then keep tracking the health status for those clients. This is all done in the controller, which is responsible for discovery, tracking clients through the proper APIs. The example above involves Kubernetes, but, in general, the same mechanism applies to every other environment. The only client change is for the grpc client to match its own host:port against "hosts". A proper config should have either "percentage" or "hosts", not both. Or maybe the latter always wins. The idea is that you canary with a small number of clients, then switch to percentages, so that the config doesn't get bloated with tens or hundreds of hostnames.

This approach has also the advantage that, if you have N groups of clients (e.g. three different frontend services that talk to a shared database), you can treat them and push to each of them independently. "clientLanguage" might be too coarse, especially when all your clients are in the same language. :-)