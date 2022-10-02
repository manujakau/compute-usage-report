## Compute-Usage-Report
AWS Lambda base tool for generate cost and usage reports

### Create assume-role in associate accounts
- Cretae role in each aws account that required to assume from master aws account.
- Select trusted entity as master account ID.
- Add cost and usage access to the statement action. Something similer to below statement.
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Action": [
                "ce:*"
            ],
            "Resource": [
                "*",
                "arn:aws:iam::*:role/AWS_Events_Invoke_Targets"
            ],
            "Effect": "Allow"
        }
    ]
}
```

### Cloudformation deployment
- Clone Repository and navigate into deployment directory.
- Update ssm parameters before deploy. 
    - ParentRegion : default region.
    - UsageReportBucket : archive bucket.
    - UsageReportAccountList : string separeated using coma of associate account ids (ex: "111122223333,444455556666").
    - UsageReportCrossAccountAssumeRole : assumerole name from associate accounts.
    - UsageReportDestinationEmail : recipient email address.
- Use deploy commandline to deploy each stack.
```
cd deployment/
./deploy [preferd-stack-name-here] [stack-to-deploy(env/infra)] [stack-action(create/update)]

ex: ./deploy report-env env create
```