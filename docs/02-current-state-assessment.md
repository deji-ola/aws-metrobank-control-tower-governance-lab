## Control Tower status (post-decommission)

- Control Tower console in us-east-1 shows a banner confirming the previous landing zone has been decommissioned.
- The main page presents an “Enable AWS Control Tower” option, meaning no active landing zone exists.
- AWS documentation notes that manual cleanup of certain resources (log buckets, CloudTrail log groups, OUs) is required after decommissioning and before re-enabling the landing zone.

## Control Tower status (post-decommission)

- Control Tower console in us-east-1 shows a banner confirming the previous landing zone has been decommissioned.
- The main page presents an "Enable AWS Control Tower" option, meaning no active landing zone exists.
- AWS documentation notes that manual cleanup of certain resources (log buckets, CloudTrail log groups, OUs) is required after decommissioning and before re-enabling the landing zone.

## Control Tower S3 logging buckets (pre-cleanup)

- Reviewed S3 buckets in us-east-1 and other Regions.
- No buckets found with reserved Control Tower names such as aws-controltower-logs-* or aws-controltower-s3-access-logs-*.
- Existing buckets are from previous labs (CloudFormation, Elastic Beanstalk, Athena, SageMaker, static website, etc.), so no S3 cleanup is required for Control Tower re-enablement at this stage.

## CloudWatch log groups (pre-cleanup)
- Searched for aws-controltower/CloudTrailLogs in us-east-1.
- Log group not present; no CloudWatch cleanup required.

