# Route 53 setup for game.castalia.institute

DNS for **game.castalia.institute** is managed in the **custodian** AWS account's `castalia.institute` hosted zone.

**Zone:** `castalia.institute` — hosted zone ID **Z088198297W8TWOSZTA9** (use `AWS_PROFILE=custodian`).

## DNS record

| Field           | Value                        |
|-----------------|------------------------------|
| **Record type** | CNAME                        |
| **Name**        | `game`                       |
| **Value**       | `InquiryInstitute.github.io` |
| **TTL**         | 300                          |

## AWS CLI (custodian profile)

```bash
export AWS_PROFILE=custodian

# List hosted zones
aws route53 list-hosted-zones --query "HostedZones[?contains(Name, 'castalia.institute')].{Name:Name,Id:Id}" --output table

# Create or update the CNAME
aws route53 change-resource-record-sets --hosted-zone-id Z088198297W8TWOSZTA9 --change-batch '{
  "Changes": [{
    "Action": "UPSERT",
    "ResourceRecordSet": {
      "Name": "game.castalia.institute",
      "Type": "CNAME",
      "TTL": 300,
      "ResourceRecords": [{ "Value": "InquiryInstitute.github.io" }]
    }
  }]
}'
```

## Verify

```bash
dig CNAME game.castalia.institute +short
```

Expected: `InquiryInstitute.github.io.`

## Summary

- **AWS CLI profile:** `custodian`
- **Hosted zone:** castalia.institute → **Z088198297W8TWOSZTA9**
- **CNAME:** `game.castalia.institute` → `InquiryInstitute.github.io`
- **Repo:** https://github.com/InquiryInstitute/game
- **Custom domain:** https://game.castalia.institute
