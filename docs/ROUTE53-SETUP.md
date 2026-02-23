# Route 53 setup for game.inquiry.institute (syzygyx account)

This repo is the source for **game.inquiry.institute**. GitHub Pages is already configured with that custom domain. To finish setup, add the DNS record in **AWS Route 53** using the **syzygyx** account.

## Prerequisites

- AWS Console access for the **syzygyx** account
- A Route 53 **hosted zone** for **inquiry.institute** (create one if it doesn’t exist)

## DNS record to add

**Subdomain:** `game.inquiry.institute` → GitHub Pages (organization project site)

| Field        | Value                      |
|-------------|----------------------------|
| **Record type** | CNAME                   |
| **Name**    | `game` (or `game.inquiry.institute` if your UI uses FQDN) |
| **Value**   | `InquiryInstitute.github.io` |
| **TTL**     | 300 (or default)          |

## Steps in Route 53 (syzygyx)

1. Log in to **AWS Console** → **Route 53** (syzygyx account).
2. Open **Hosted zones** and select the hosted zone for **inquiry.institute**.
3. Click **Create record**.
4. Set:
   - **Record name:** `game`
   - **Record type:** `CNAME`
   - **Value:** `InquiryInstitute.github.io`
   - **TTL:** 300 (or leave default)
5. Create the record.

## Verify

- Propagation can take up to 24 hours (often minutes).
- In the repo: **GitHub** → **Settings** → **Pages** → “Custom domain” should show a successful DNS check for `game.inquiry.institute`.
- After DNS is correct, enable **Enforce HTTPS** in the same Pages settings.

## Summary

- **Repo:** https://github.com/InquiryInstitute/game  
- **Pages (default URL):** https://inquiryinstitute.github.io/game/  
- **Custom domain:** https://game.inquiry.institute (after Route 53 CNAME is in place)
