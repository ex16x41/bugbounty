The bug name which I found was “Password Reset Link Not Expired After Use”. This comes under the VRT of “Insufficient Security Configurability >Weak Reset Password Implementation > Token Not Invalidated After Use”

Steps To Find This Bug:

    Go to https://target.com/ password reset page.
    Enter your email, and ask for a password reset link.
    Now go to mail and open that link in two tabs.
    Reset the password from one tab, reload the other tab , and if it let’s you reset password again then it is vulnerable to token not invalidated after use as we are resetting the password two times with same token.

Impact/Exploit Scenario: If victim’s email account is still logged into his/her Office Computers or any public Internet Café. Then any external attacker can use the used token to reset victims password.

Severity: Now due to this difficult to happen exploit scenario , which requires user interaction it is given as a P4 bug under Bugcrowd VRT.

Now this feature can be also used to sometimes chain it with other vulnerabilities, to get higher severity depending on the functionalities present in the website.
