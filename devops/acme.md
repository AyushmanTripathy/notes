# ACME

- Automatic Certificate Management Environment
- Its a protocol to prove control of domain & obtain TLS certificates
- Certificate Authority (CA like Let's Encrypt) support ACME

| Component     | What it is            | Role                                                         |
| ------------- | --------------------- | ------------------------------------------------------------ |
| Let's Encrypt | Certificate Authority | Issues TLS certificates and provides an ACME server          |
| Certbot       | ACME client           | Runs on your server and talks to Let's Encrypt's ACME server |

## Flow

1. Client creates ACME account with CA
2. Client requests certificate to CA
3. CA issues a challange to Client, so that it proves the ownership of domain
4. Client completes challange using one of mechanisms
    - Ex. `DNS-01`: Adding a TXT record.
    - `HTTP-01`: Explosing a certain HTTP endpoint (`/.well-known/acme-challange`, port needs to be free)
    - Performing a specific TLS handshake
5. CA issues a certificate
6. Client automatically repeats process before expiration

## Built in ACME Clients

- Caddy and Traefik have built in ACME support
- cert-manager in Azure Kubernetes service does ACME
- hence Certbot is not required.
