## Task

You and your team are working on a project in AWS. At the very beginning, you just created resources by clicking in the Developer Console, but as your project grew, you found it problematic to remember all the steps needed every time. You decided to start from scratch and use an automation tool so that you can easily create multiple environments, or recreate them if something bad happens.

You and your team have decided to go with Terraform. The first elements that need to be created are the S3 bucket and the SQS queue. These elements are connected together because the queue should be notified when someone uploads any file to S3.

You have prepared the requirements and now you're ready to implement them in Terraform.

### Objectives

- There should be an S3 bucket referenced in Terraform as `bucket` and named `upload-bucket`. The ACL should be `private`.
- There should be an SQS queue referenced in Terraform as `queue` and named `upload-queue`.
- The above queue should have a delay specified as `60 seconds`, a max message size of `8KiB`, should discard messages after `48 hours` and should wait for up to 15 seconds for messages to be received.
- There should be an IAM policy document created as Terraform `data`, referenced as `iam_notif_policy_doc`, which should describe the policy that will be used by the bucket notification hook to post messages to the queue, or you can use EOF expression in policy and omit this step.
- The above document should contain one statement with it equal to `1`.
- The above statement should work only for `upload-bucket` and it should be tested by checking if the source ARN matches.
- The above statement should work only on `upload-queue` and it should allow messages to be sent to it.
- The above statement should use the `AWS` type of principal with identifiers set to `*`.
- The above document should be used to create the `upload-queue` policy referenced in Terraform as `notif_policy`. You may as well use inline policy implementing the same thing instead of using policy document.
- Finally, bucket notification should be enabled (referenced in Terraform as `bucket_notif`) to send a message to `upload-queue` when an object is created in `upload-bucket`.
- All references to other resources should be specified as Terraform identifiers, not as text.
