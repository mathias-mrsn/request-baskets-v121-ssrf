# SSRF Vulnerability Exploit for Request-Baskets (CVE-2023-27163)

This repository presents an exploit demonstrating the Server-Side Request Forgery (SSRF) vulnerability identified as [CVE-2023-27163](https://nvd.nist.gov/vuln/detail/CVE-2023-27163) in the [request-baskets](https://github.com/darklynx/request-baskets) project, up to [version 1.2.1](https://github.com/advisories/GHSA-58g2-vgpg-335q). Exploiting this vulnerability enables attackers to forward HTTP requests to an internal/private HTTP service.

## How It Operates ?

This exploit calls the API component `/api/baskets/{name}`. This component creates a new basket with a specified name. This component initiates a POST request with a specified body schema.

```json
{
  "forward_url": "https://myservice.example.com/events-collector",
  "proxy_response": false,
  "insecure_tls": false,
  "expand_path": true,
  "capacity": 250
}
```

If we change the `forward_url` to a local service and set the `proxy_response` to `true`, we can create a local proxy for HTTP requests on the targeted machine.
## Usage

```shell
wget https://raw.githubusercontent.com/mathias-mrsn/CVE-2023-27163/master/exploit.py
python3 exploit.py <public_url> <targeted_url>
```

---
This exploit has been coded for the HTB machine `Sau`.
