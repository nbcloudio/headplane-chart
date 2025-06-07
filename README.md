# headplane

![Version: 0.1.0](https://img.shields.io/badge/Version-0.1.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 0.6.0](https://img.shields.io/badge/AppVersion-0.6.0-informational?style=flat-square)

This helm chart deploys [Headplane](https://github.com/tale/headplane) + [Headscale](https://github.com/juanfont/headscale) and an embedded Tailscale relay in a kubernetes cluster.

### OIDC Configuration

To use OIDC, you must provide the OIDC client secrets via Kubernetes secret:

- Create a secret named `oidc-secrets` with keys `oidc_headplane_client_secret` and `oidc_headscale_client_secret`.

```sh
kubectl create secret generic oidc-secrets \
  --from-literal=oidc_headplane_client_secret=your-headplane-oidc-client-secret \
  --from-literal=oidc_headscale_client_secret=your-headscale-oidc-client-secret \
  -n <namespace>
```


## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| headplane.config.headscale.config_path | string | `"/etc/headscale/config.yaml"` |  |
| headplane.config.headscale.config_strict | string | `"true"` |  |
| headplane.config.headscale.url | string | `"https://vpn.example.com"` |  |
| headplane.config.integration.kubernetes.enabled | bool | `true` |  |
| headplane.config.integration.kubernetes.pod_name | string | `"headplane-0"` |  |
| headplane.config.integration.kubernetes.validate_manifest | bool | `true` |  |
| headplane.config.oidc.client_id | string | `"REPLACE_IT_WITH_YOUR_OIDC_CLIENT_ID_FOR_HEADPLANE"` |  |
| headplane.config.oidc.disable_api_key_login | bool | `true` |  |
| headplane.config.oidc.enabled | bool | `false` |  |
| headplane.config.oidc.issuer | string | `"https://your-oidc-issuer-url.com"` |  |
| headplane.config.oidc.redirect_uri | string | `"https://your-headplane-admin-domain.com/admin/oidc/callback"` |  |
| headplane.config.oidc.token_endpoint_auth_method | string | `"client_secret_post"` |  |
| headplane.config.server.cookie_secure | bool | `true` |  |
| headplane.config.server.host | string | `"0.0.0.0"` |  |
| headplane.config.server.port | int | `3000` |  |
| headplane.image | string | `"ghcr.io/tale/headplane:0.6.0"` |  |
| headplane.secret.create | bool | `true` |  |
| headplane.secret.name | string | `"headplane-secret"` |  |
| headscale.acl | string | `"{\n  \"acls\": []\n}\n"` |  |
| headscale.config.database.debug | bool | `false` |  |
| headscale.config.database.sqlite.path | string | `"/etc/headscale/db.sqlite"` |  |
| headscale.config.database.type | string | `"sqlite"` |  |
| headscale.config.derp.paths | list | `[]` |  |
| headscale.config.derp.server.automatically_add_embedded_derp_region | bool | `true` |  |
| headscale.config.derp.server.enabled | bool | `false` |  |
| headscale.config.derp.server.ipv4 | string | `"1.2.3.4"` |  |
| headscale.config.derp.server.ipv6 | string | `"2001:db8::1"` |  |
| headscale.config.derp.server.private_key_path | string | `"/var/lib/headscale/derp_server_private.key"` |  |
| headscale.config.derp.server.region_code | string | `"headscale"` |  |
| headscale.config.derp.server.region_id | int | `999` |  |
| headscale.config.derp.server.region_name | string | `"Headscale Embedded DERP"` |  |
| headscale.config.derp.server.stun_listen_addr | string | `"0.0.0.0:3478"` |  |
| headscale.config.derp.urls[0] | string | `"https://controlplane.tailscale.com/derpmap/default"` |  |
| headscale.config.dns.base_domain | string | `"headscale.vpn"` |  |
| headscale.config.dns.magic_dns | bool | `true` |  |
| headscale.config.dns.nameservers.global[0] | string | `"1.1.1.1"` |  |
| headscale.config.dns.nameservers.global[1] | string | `"8.8.8.8"` |  |
| headscale.config.grpc_allow_insecure | bool | `false` |  |
| headscale.config.grpc_listen_addr | string | `"0.0.0.0:50443"` |  |
| headscale.config.listen_addr | string | `"0.0.0.0:8080"` |  |
| headscale.config.metrics_listen_addr | string | `"0.0.0.0:9090"` |  |
| headscale.config.noise.private_key_path | string | `"/etc/headscale/noise_private.key"` |  |
| headscale.config.oidc.client_id | string | `"YOUR_OIDC_CLIENT_ID_FOR_HEADSCALE"` |  |
| headscale.config.oidc.enabled | bool | `false` |  |
| headscale.config.oidc.issuer | string | `"https://your-oidc-issuer.com"` |  |
| headscale.config.policy.mode | string | `"database"` |  |
| headscale.config.policy.path | string | `"/etc/headscale/acl.hujson"` |  |
| headscale.config.prefixes.allocation | string | `"sequential"` |  |
| headscale.config.prefixes.v4 | string | `"100.64.0.0/10"` |  |
| headscale.config.prefixes.v6 | string | `"fd7a:115c:a1e0::/48"` |  |
| headscale.config.server_url | string | `"https://vpn.example.com"` |  |
| headscale.image | string | `"headscale/headscale:0.25.1"` |  |
| headscale.secret.create | bool | `true` |  |
| headscale.secret.name | string | `"headscale-secret"` |  |
| ingress.className | string | `"nginx"` |  |
| ingress.enabled | bool | `false` |  |
| ingress.headplaneDomain | string | `"headplane.example.com"` |  |
| ingress.headscaleDomain | string | `"vpn.example.com"` |  |
| ingress.labels | list | `[]` |  |
| ingress.tlsSecretName | string | `"headplane-tls"` |  |
| namespace | string | `"headplane"` |  |
| pvc.accessModes[0] | string | `"ReadWriteOnce"` |  |
| pvc.enabled | bool | `true` |  |
| pvc.name | string | `"headscale-config"` |  |
| pvc.storage | string | `"1Gi"` |  |
| relay.config.advertise_exit_node | string | `"true"` |  |
| relay.config.authKey | string | `""` |  |
| relay.config.exit_node | string | `"example.com"` |  |
| relay.config.firewall_debug | string | `"false"` |  |
| relay.config.hostname | string | `"example.com"` |  |
| relay.config.login_server | string | `"https://vpn.example.com"` |  |
| relay.config.routes | string | `"10.0.0.0/8"` |  |
| relay.enabled | bool | `false` |  |
| relay.image | string | `"ghcr.io/tailscale/tailscale:v1.80.3"` |  |
| relay.pvc.accessModes[0] | string | `"ReadWriteOnce"` |  |
| relay.pvc.enabled | bool | `false` |  |
| relay.pvc.name | string | `"tailscale-relay-data"` |  |
| relay.pvc.storage | string | `"1Gi"` |  |

