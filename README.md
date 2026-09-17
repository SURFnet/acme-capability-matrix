# ACME Capability Matrix

A community list of ACME clients, appliances and server-side platforms, and their support of advanced functionality.

[SURF&#39;s ACME knowledge base page](https://servicedesk.surf.nl/wiki/spaces/WIKI/pages/147098524/ACME).

What we care about:

- **ACME: ***How* the platform can get certificates over ACME
- **EAB: ** If it supports External Account Binding ([RFC 8555 §7.3.4](https://www.rfc-editor.org/rfc/rfc8555#section-7.3.4)) for CA’s other than Let’s Encrypt.
- **ARI: **ACME Renewal Information ([RFC 9773](https://www.rfc-editor.org/info/rfc9773/)) for CA control of renewal. 

## Legend

**ACME mode**, how ACME is supported:

| Value       | Meaning                                                                                            |
| ----------- | -------------------------------------------------------------------------------------------------- |
| `native`  | ACME is built into the product.                                                                    |
| `sidecar` | No native ACME; known implementations with a client next to it and deployed via API / hook / SSH. |
| `planned` | Vendor has announced/committed to ACME, not shipped.                                               |
| `none`    | No current ACME support, manual certificate management.                                            |

**EAB / ARI**, if it supports enterprise features:

| Value       | Meaning                              |
| ----------- | ------------------------------------ |
| `yes`     | Verified supported.                  |
| `partial` | Supported with caveats — see Notes. |
| `no`      | Verified not supported.             |
| `planned` | Announced/committed, not shipped.    |
| `?`       | Not verified yet.                    |

## ACME clients & libraries

| Platform                                             | EAB     | ARI    | Notes                                                                |
| ---------------------------------------------------- | ------- | ------ | -------------------------------------------------------------------- |
| [certbot](https://certbot.eff.org/)                   | `yes` | ?      | EFF; de-facto standard on Linux/Unix.                                |
| [acme.sh](https://github.com/acmesh-official/acme.sh) | `yes` | ?      | Pure-shell POSIX client.                                             |
| [dehydrated](https://dehydrated.io/)                  | `yes` | ?      | Bash + OpenSSL, very few dependencies.                               |
| [lego](https://go-acme.github.io/lego/)               | `yes` | ?      | Go, single binary, minimal dependencies.                             |
| [Certify The Web](https://certifytheweb.com/)         | `yes` | ?      | Windows GUI client.                                                  |
| [simple-acme](https://simple-acme.com/)               | `yes` | ?      | Windows; the maintained fork/successor of win-acme.                  |
| [win-acme](https://www.win-acme.com/)                 | `yes` | `no` | No ARI support — no longer works reliably; use simple-acme instead. |

## Appliances & server-side platforms

| Platform                                                                                             | ACME            | EAB         | ARI | Notes                                                                                                                                                                   |
| ---------------------------------------------------------------------------------------------------- | --------------- | ----------- | --- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Ansible](https://docs.ansible.com/projects/ansible/latest/index.html)                                | `native`      | ?           | ?   | Use the [acme_certificate module](https://docs.ansible.com/ansible/latest/collections/community/crypto/acme_certificate_module.html) from the community.crypto module. |
| [Kubernetes](https://kubernetes.io/)                                                                  | `native`      | ?           | ?   | [cert-manager](cert-manager.io) is the de-facto standard.                                                                                                               |
| [Citrix NetScaler ADC](https://www.netscaler.com/)                                                    | `sidecar`     | ?           | ?   | No native ACME; run certbot/dehydrated/lego on a helper Linux host.                                                                                                     |
| [F5 BIG-IP](https://www.f5.com/products/big-ip-services)                                              | `native`      | ?           | ?   | Via F5's own[Kojot ACME](https://github.com/f5devcentral/kojot-acme) (a dehydrated wrapper).                                                                             |
| [Fortinet ADC (FortiADC)](https://www.fortinet.com/products/application-delivery-controller/fortiadc) | `native`      | `partial` | ?   | When using EAB, the DNS-01 challenge cannot be disabled.                                                                                                                |
| [HAProxy](https://www.haproxy.org/)                                                                   | `native`      | ?           | ?   | Built-in support for acme.sh.                                                                                                                                           |
| [HashiCorp Vault](https://developer.hashicorp.com/vault/docs/secrets/pki/acme)                        | `native`      | ?           | ?   | ACME**server role** via the PKI secrets engine (not a client).                                                                                                    |
| [Kemp LoadMaster](https://kemptechnologies.com/)                                                      | `native`      | ?           | ?   |                                                                                                                                                                         |
| [Osiris (CACI)](https://www.caci.nl/osiris/)                                                          | `unsupported` | ?           | ?   | ACME only for new instances, "somewhere in 2026" for existing customers                                                                                                 |
| [VMware Unified Access Gateway](https://www.vmware.com/products/unified-access-gateway.html)          | `manual`      | ?           | ?   |                                                                                                                                                                         |
