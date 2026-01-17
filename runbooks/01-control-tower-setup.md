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

1. In the us-east-1 Region, open the S3 console and list all buckets.
2. Verify whether any buckets exist with reserved AWS Control Tower names:
   - aws-controltower-logs-*
   - aws-controltower-s3-access-logs-*
3. Result for this org:
   - No buckets found with Control Tower reserved names.
   - Existing buckets belong to previous labs (CloudFormation, Elastic Beanstalk, Athena, SageMaker, static websites, etc.), so no S3 cleanup is required for Control Tower.
4. Open CloudWatch → Logs → Log groups in us-east-1.
5. Search for the log group **aws-controltower/CloudTrailLogs**.
6. Result for this org:
   - Log group **not present**; no CloudWatch cleanup required before re-enabling Control Tower.
7. Record these findings in `docs/02-current-state-assessment.md` under "Control Tower S3 logging buckets (pre-cleanup)" and "CloudWatch log groups (pre-cleanup)" for auditability.
#### 3.2 Configure governed Regions

4. In the "Governed Regions" section, select:
   - Home Region (pre-selected): us-east-1.
   - Additional governed Region: eu-west-2 (London).
5. Rationale:
   - us-east-1 hosts Control Tower’s home-region services and shared governance components.
   - eu-west-2 is the primary workload Region for UK banking workloads, aligning with Metro Bank’s data residency expectations.
6. Leave all other Regions unchecked to reduce complexity and operational overhead for this POC.
7. Click **Next** to move to "Create organizational units (OUs)".

#### 3.3 Create organizational units (OUs)
8. Control Tower proposes creating 2 foundational OUs under Root:
   - **Security** (for log-archive and audit accounts) - Status: "Not created"
   - **Sandbox** (recommended for dev/test workloads) - Status: "Not created"  
9. **Action**: Click **"Create OUs"** button.
10. Wait for both OUs to show **"Created"** status.
11. Metro Bank alignment:
    - Security OU: will contain log-archive, security-audit accounts
    - Sandbox OU: for non-production experimentation
    - Existing Prod/Testing OUs remain under Root (to be refined later)
12. Click **Next** → proceed to "Configure Service integrations".

#### 3.4 Configure Service integrations (optional)
13. **AWS Config for detective controls**: Clicked **"Disable AWS Config"**.
    - Aggregator account field requires 12-digit account ID (not available yet).
14. **AWS CloudTrail Centralized logging**: Clicked **"Disable AWS CloudTrail"**.
    - CloudTrail administrator field requires account ID (not available yet).
15. **Rationale**: 
    - Optional integrations requiring non-existent accounts cannot be configured now.
    - Core Control Tower landing zone (OUs, guardrails, basic logging) sufficient for Metro Bank POC.
    - Cost control: avoids additional Config/CloudTrail aggregator setup.
16. Clicked **Next** → proceed to "Review and enable AWS Control Tower".

