# IAM

#### Permission: Only 1 instance for 1 person, 특정 인원에게 특정 인스턴스를 사용할 권한 부여.
* Create custom permission and set permission as below.
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "TheseActionsDontSupportResourceLevelPermissions",
            "Effect": "Allow",
            "Action": ["ec2:Describe*"],
            "Resource": "*"
        },
        {
            "Sid": "TheseActionsSupportResourceLevelPermissions",
            "Effect": "Allow",
            "Action": [
                "ec2:RunInstances",
                "ec2:TerminateInstances",
                "ec2:StopInstances",
                "ec2:StartInstances"
            ],
            "Resource": "arn:aws:ec2:region:accountid:instance/*"
        }
    ]
}
```
* Reference
  * https://stackoverflow.com/questions/32560343/assign-iam-user-to-access-only-one-ec2-instance
  * https://aws.amazon.com/blogs/security/demystifying-ec2-resource-level-permissions/

#### Permission: Only 1 S3 storage for 1 person. 특정 인원에게 특정 S3 저장소를 사용할 권한 부여
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": "s3:ListBucket",
            "Resource": "arn:aws:s3:::bucket-name"
        },
        {
            "Sid": "VisualEditor1",
            "Effect": "Allow",
            "Action": [
                "s3:PutObject",
                "s3:GetObject",
                "s3:DeleteObject"
            ],
            "Resource": "arn:aws:s3:::bucket-name/*"
        }
    ]
}
```
* Reference
  * https://aws.amazon.com/ko/premiumsupport/knowledge-center/s3-console-access-certain-bucket/
