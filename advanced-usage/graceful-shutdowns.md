# 🛑 Graceful Shutdowns & Traffic Monitoring

If you run pWS standalone in a cluster, at scale, you might run into capacity issues: RAM usage might be near the limit and even if you decide to horizontally scale the pods, new connections might still come to pods that are near-limit and run into OOM at some point.

For Kubernetes, running [Network Watcher 4.0+](../network-watcher/getting-started.md) inside the same pod will solve the issues by continuously checking the current pod using a "usage endpoint" (**Prometheus Server is not needed**), labeling the pods that get over a specified threshold.

pWS is also embedded with a graceful shutdown operator. This means that upon closing the server, it closes all the active connections and tells them to reconnect again. When using Network Watcher, this is done automatically within the assigned pods in Kubernetes at the service and pod level. More details can be found on the [Network Watcher documentation](../network-watcher/getting-started.md).