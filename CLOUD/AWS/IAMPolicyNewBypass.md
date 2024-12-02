I discovered a method to bypass IAM policy restrictions on AWS Secrets Manager. By using direct API calls, secrets can be accessed even when policies enforce access only via the web console or AWS CLI—successfully bypassing StringNotLike conditions for aws:UserAgent.

While API calls are well-documented in AWS as a general concept, this practical technique highlights a real-world vulnerability in IAM policy configurations. If policies allow viewing secret values of user (authenticated via credentials in aws cli), this method can universally bypass restrictions that block CLI requests.

Test Case: This was tested on a lab sts:GetFederationToken to access the web console for retrieving a secret flag. Instead of using the console, or generating temp creds for console access-> the secret was extracted directly via API by sending an HTTPS POST Request to SecretsManager (with Sigv4) This technique might be prevented by multi-factor authentication or stricter policies, such as enforcing specific aws:SourceIp.

Security Improvement: Stricter IAM policies, like allowing requests only from specific IP ranges or host, could mitigate this. However, attackers might explore spoofing as a potential bypass.

Link ot my PR on HackTricks Git : https://github.com/HackTricks-wiki/hacktricks-cloud/pull/116
