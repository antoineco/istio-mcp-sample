# Istio MCP-over-XDSv3 server sample

A sample implementation of a [MCP-over-XDSv3][mcp-design] gRPC server for Istio.

## Usage

To build and publish the container image and deploy the server to Kubernetes using the generated container image,
install [ko][ko] locally, then apply the deployment manifest:

```
ko apply -f deploy.yaml
```

Then, configure the server as an `istiod` [configSource][istio-cfgsrc]:

```yaml
apiVersion: install.istio.io/v1alpha1
kind: IstioOperator
spec:
  profile: minimal
  meshConfig:
    configSources:
    - address: xds://mcp-sample.default.svc.cluster.local:15010
    - address: k8s://
# ...
```

[mcp-design]: https://docs.google.com/document/d/1lHjUzDY-4hxElWN7g6pz-_Ws7yIPt62tmX3iGs_uLyI/
[ko]: https://ko.build/
[istio-cfgsrc]: https://istio.io/latest/docs/reference/config/istio.mesh.v1alpha1/#ConfigSource
