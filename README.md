# dns-override
Repo in use to fix broken DNS implementation with the Bosh Noble stemcell

## Operator file

This is the operator file we have in use by our bosh-deployment

```yaml
# This ops-file ensures Noble stemcells (Ubuntu 24.04) have correct DNS configuration
# It adds explicit DNS servers for the Director VM network

# Add the dns-fix job to the Director instance group
- type: replace
  path: /instance_groups/name=bosh/jobs/-
  value:
    name: dns-override
    release: dns-override
    properties:
      dns_override:
        nameservers: ((internal_dns))


# Add the dns-fix release to the BOSH Director
- type: replace
  path: /releases/-
  value:
    name: dns-override
    version: "8"
    url: https://github.com/rmeerdink/dns-override/releases/download/8/dns-override-8.tgz
    sha1: sha256:594ac464814e121fdf17a1ba6fceb7f7085630f95f093efdd6b8bcb2d61f1305
```
