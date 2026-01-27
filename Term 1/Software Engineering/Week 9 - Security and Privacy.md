# Software security
Software security should always be a high priority for a product developers and their users.
# Operation Security
Operational Security focuses on helping users to maintain security. User attacks try to trick users into disclosing their credentials or accessing a website that includes malware such as a key-logging system.
## Mitigation Practices
- Auto-logout
- User command logging
- Multi-factor authentication
# Injection Attack
Injection attacks are a type of attack where a malicious user uses a valid input field to input malicious code or database commands.
These malicious instructions are then executed, causing some damage to the system. Code can be injected that leaks systems to the attackers
## Preventing SQL Injection
Prepared Statements (Parameterized Queries)
Stored Procedures
Input Validation and Escaping
## Cross-Site Scripting
XSS is another form of injection attack

Attacker inject malicious JS code to the webpage that is returned from a server to a client and this script is executed when the page is displayed in the user's browser
(Use Cookies to steal personal data)

# Session Hijacking Attack
When user authenticates themselves attackers will try to hijack the session created from authentication
Typically attacked through XSS injection to target cookies that contain session token

# Actions To reduce likelihood of hacking
## Traffic Encryption
Encrypting network traffic between clients and your server. this means using https over http. 
## Multifactor authentication
Always use MFA for new actions that may be damaging
## Short timeouts
Use relatively short timeouts on sessions. If no activity on session in a short time redirect to authentication page.
# Denial of Service Attacks
DOS attacks are to make a service unavailable for normal use.
# Brute Force Attacks
Try many times to guess password(can lead into a DOS attack)
# Federated Identity
Oauth, use google or Microsoft to authenticate for you or SSO