# CNAME
## 🌐 What is CNAME?

**CNAME** stands for **Canonical Name**. It is a type of **DNS (Domain Name System) record** used to create an **alias (another name)** for an existing domain or hostname.

In simple terms:

> **CNAME says: “This hostname is another name for that hostname.”**

### 🔹 Simple example

Suppose you have:

```text
example.com
```

and your web server is actually hosted at:

```text
server.example-host.com
```

You could configure:

```text
www.example.com  →  CNAME  →  server.example-host.com
```

So when someone visits:

```text
www.example.com
```

DNS tells them that `www.example.com` is an alias for `server.example-host.com`.

![Image](https://images.openai.com/static-rsc-4/70PY_9YoeW7sCyAYc0LGuW3QE58ozQVYejUuuvVfOYgSxop9vUtuVynvkWz02HAv91XdYfRVloGwYUozdUme5-CyXPnR7NoCRKbkcdpbtebtQVc6YUQgf2QpeqyKy8miTWIq_D9J3QLHdgme-ENTdV4FIAxiM4DG3rf8TmS1xqOp09GS-ldZEr0kTu_ouaZA?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/FzeAtcClFCAKF1XvyVGANGq1TAR5WgOohm6IowV5YgD8EUeU89gXvOL35x9hWJedPM7gD-sNx3e27_p1Mex5U9aONHOyw6q-FC_eBwIe4sgj7ZEZjScjoeghk9toSDWba9jdh2wukTIgm4qZuLnD-A8X4Ufe1g2aG1bU-vG6TkADNPEkemVsbp5oinRDsUxs?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/m72RaK_03SUZFMdDXOP2cqW4FxEYQIeigoe_PPYJVSdYLLK3wZmE6ZlxRHSssnMaejf8mtEVYJSzJOirdDodrYb1vfsSo3wQJtqtEnsoJ1dkIrYbWGI3MwOfannnJjVwcWdliBqWkJz5vXv0r9yd3_BLnVjoyV3GyO2ohusLOKek_BTy1iNjkM93F9tRYnrG?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/nTBDcJcXm4thjtR0URRtHGZL1DC-jziwsFHq-dMM9uOMt1z8BjYH63Mx2anQE8IMOW66xgEKb76f44hLqF2oTj_Tmr_EM1d6w2Jzeu_h0c-OXOCw3FLPOSg1il3ENaYKp1jicP5UKGol65qQJr_uYyQPHbHZZGigOPton4t8RbP7r_GKDWb0Lr2DSQGA4kjP?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/n8nRL2SbkrtVb9wQzKvYrfipzvsMJwCc_vfLW7_2XfMUxJf7VDCAvDFHEzXMfP9xd9hk0mWdtpw5orQix2hU4z86zcI0_mM0q86ITm4wKUICyhdwWrKEwxHM9ccgFsPXX2FpCIxSiFZOR_paYNY2qL1kOLrgD_OS3ehUXmURN50RHHLg--ula30V3GeGVog8?purpose=fullsize)

---

## 🧩 CNAME structure

A DNS zone might contain:

| Name               | Type  | Target               |
| ------------------ | ----- | -------------------- |
| `www.example.com`  | CNAME | `example.com`        |
| `blog.example.com` | CNAME | `blog.hosting.com`   |
| `shop.example.com` | CNAME | `shops.provider.com` |

For example:

```text
www.example.com CNAME example.com
```

This means:

```text
www.example.com
       ↓
    CNAME
       ↓
example.com
```

DNS then resolves the target (`example.com`) to its final IP address.

---

## 🔥 CNAME vs A record

This distinction is very important when learning web security and reconnaissance.

### A Record

An **A record** maps a hostname directly to an IPv4 address:

```text
example.com → 203.0.113.10
```

### CNAME Record

A **CNAME** maps one hostname to another hostname:

```text
www.example.com → example.com
```

Think of it as:

```text
A record:
Name → IP address

CNAME:
Name → Another hostname
```

---

## 🎯 Why CNAME records are useful

CNAMEs are commonly used for:

### 1. 🌍 Subdomains

```text
blog.example.com → example.wordpress.com
```

The blog can be hosted by another provider while still using your domain.

### 2. ☁️ Cloud services

For example:

```text
app.example.com → some-service.cloud-provider.com
```

### 3. 📦 CDNs

A domain might point through a CDN:

```text
cdn.example.com
       ↓
CNAME
       ↓
provider.cdn.example
```

### 4. 📧 SaaS services

Companies often use CNAMEs when connecting services such as email, marketing, authentication, or website platforms.

---

# 🔐 Why CNAME matters in cybersecurity

Since you're learning **web security/reconnaissance**, CNAME records are particularly interesting.

During reconnaissance, you may discover:

```text
dev.example.com → dev-host.company-cloud.com
```

or:

```text
support.example.com → company.zendesk.com
```

This can reveal **which external service or hosting provider is being used**.

### Example

Imagine:

```text
support.example.com
        ↓
CNAME
        ↓
company.zendesk.com
```

A security researcher can identify that the organization's support portal is using **Zendesk**.

Similarly:

```text
static.example.com
        ↓
CNAME
        ↓
something.cloudflare.net
```

could indicate the use of a CDN/proxy service.

---

## ⚠️ CNAME and subdomain takeover

One important security issue associated with CNAMEs is **subdomain takeover**.

For example:

```text
old.example.com
      ↓
CNAME
      ↓
old-app.somecloudservice.com
```

Suppose the organization deletes its cloud application but forgets to remove the DNS record.

Now:

```text
old.example.com
      ↓
CNAME
      ↓
old-app.somecloudservice.com
      ↓
❌ Resource no longer exists
```

Depending on the service and its configuration, an attacker might potentially claim the abandoned resource and serve content through:

```text
old.example.com
```

This is why **dangling CNAME records** are an important thing to investigate during authorized security testing.

---

## 🔎 How to check CNAME records

On Linux/Kali/Parrot OS:

### `dig`

```bash
dig CNAME www.example.com
```

Or:

```bash
dig www.example.com
```

Look for something like:

```text
www.example.com.  300  IN  CNAME  example.com.
```

### `nslookup`

```bash
nslookup -type=CNAME www.example.com
```

### `host`

```bash
host -t CNAME www.example.com
```

---

## 🧠 Easy way to remember

Think of a CNAME like a **nickname**:

```text
John Smith
   ↑
real name

Johnny
   ↑
nickname
```

Similarly:

```text
example.com
   ↑
canonical/real hostname

www.example.com
   ↑
CNAME/alias
```

So:

> **CNAME = hostname → another hostname**

while:

> **A = hostname → IPv4 address**

This makes CNAME records especially useful for understanding **DNS architecture, subdomains, cloud services, CDNs, and potential dangling-DNS/subdomain-takeover issues** during authorized reconnaissance.
