# Runbook 01 – AWS Control Tower Landing Zone Setup

## Purpose

Establish a new AWS Control Tower landing zone in the training organization, simulating Metro Bank’s multi-account governance framework.

## Preconditions

- Logged into the AWS management account in the console (us-east-1 Control Tower home Region, eu-west-2 for workloads).
- AWS Organizations already enabled.
- Control Tower previously decommissioned; cleanup validated.
- Home Region: us-east-1.
- Primary workload Region for banking workloads: eu-west-2 (London).

## High-level steps

1. Review Control Tower status and banner.
2. Validate cleanup prerequisites (S3 logs bucket, CloudTrail log group, OUs).
3. Run the “Enable AWS Control Tower” wizard.
4. Verify creation of core accounts and OUs.
5. Document guardrails and default controls.

## Detailed procedure

### Step 1 – Review Control Tower status
“Navigated to AWS Control Tower in us-east-1 using the management account.”

Observed banner message confirming the previous landing zone has been decommissioned, with a link to cleanup documentation.

Confirmed Control Tower now shows the ‘Enable AWS Control Tower’ call-to-action, indicating a fresh landing zone can be created.

Recorded Control Tower home Region as us-east-1 for this training org.

### Step 2 – Validate cleanup prerequisites

(TBD)