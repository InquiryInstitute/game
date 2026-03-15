# Subdomain integration: game.castalia.institute ↔ GitHub Pages

How **game.castalia.institute** is wired to GitHub Pages.

## GitHub side

| Item              | Status |
|-------------------|--------|
| **Custom domain** | `game.castalia.institute` set in repo Settings → Pages |
| **CNAME file**    | Present in repo root (content: `game.castalia.institute`) |
| **Source**        | Branch `main`, path `/` |
| **Enforce HTTPS** | Enable after GitHub issues the certificate |

## DNS side

- **Where:** Route 53, `castalia.institute` zone (`AWS_PROFILE=custodian`)
- **Record:** CNAME `game` → `InquiryInstitute.github.io`
- **Details:** See [ROUTE53-SETUP.md](./ROUTE53-SETUP.md)

## After DNS propagates

1. GitHub auto-issues a certificate for `game.castalia.institute`.
2. Enable **Enforce HTTPS** in Settings → Pages, or via CLI:

```bash
echo '{"cname":"game.castalia.institute","https_enforced":true}' | gh api repos/InquiryInstitute/game/pages -X PUT --input -
```

## Check status

```bash
gh api repos/InquiryInstitute/game/pages
```

- `cname`: `game.castalia.institute`
- `https_enforced`: `true` after enabling

## URLs

- **Default Pages:** https://inquiryinstitute.github.io/game/
- **Custom domain:** https://game.castalia.institute
