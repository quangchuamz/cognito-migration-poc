---
inclusion: always
---

# Cross-Account Security Guidelines

## IAM Role Design
- Use temporary credentials only
- Implement role assumption with external ID
- Regular rotation of access keys
- Audit role usage regularly

## Network Security
- Use VPC endpoints where possible
- Implement network ACLs appropriately
- Monitor cross-account traffic
- Use AWS PrivateLink for sensitive communications

## Data Protection
- Encrypt all data in transit
- Use AWS KMS for encryption keys
- Implement data classification
- Regular security assessments

## Access Control
- Implement least privilege principle
- Use resource-based policies where appropriate
- Regular access reviews and audits
- Implement break-glass procedures

## Monitoring and Alerting
- Log all cross-account activities
- Monitor for unusual access patterns
- Set up alerts for security events
- Regular security posture reviews

## Compliance
- Follow organizational security policies
- Implement required security controls
- Regular compliance assessments
- Document security decisions