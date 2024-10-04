
# CVE-2023-7028

## Identification

 - The ID of this vulnerability is CVE-2023-7028.
 - A vulnerability in certain GitLab CE/EE versions that allowed password reset emails to be redirected to unverified emails.
 - Versions affected: 16.1.0–16.1.5, 16.2.0–16.2.8, 16.3.0–16.3.6, 16.4.0–16.4.4, 16.5.0–16.5.5, 16.6.0–16.6.3 and 16.7.0–16.7.1 .

## Listing

 - This vulnerability was discovered by asterion04 on the 12th of January 2024, through the HackerOne bug bounty program.
 - It was classified by CVSS with a rating of 10.0, the highest possible, and categorised as Critical.  

## Exploit

 - This is a remote exploit and uses the Burp Suite software (https://gitlab.com/gitlab-org/gitlab/-/issues/436084).
 - Convert the "Forgot Your Password?" request to JSON in Burp Suite using the Content-Type Converter plugin.
 - Modify the JSON to include both victim's and attacker's emails before forwarding the request.
 - Receive the reset link in both emails, reset the password, and log in as the victim.

## Attacks

 - If the attack is successful, the individual responsible can gain control of someone else's GitLab account.
 - This implies that they could access confidential information such as the ongoing codes, the alterations made, and login credentials.
 - Furthermore, they could utilize this compromised account to aim at a larger audience or various computer networks for further detrimental actions.
 - No attacks were executed before the vulnerability was patched.
