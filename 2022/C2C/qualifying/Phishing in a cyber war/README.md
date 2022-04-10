# Phishing in a cyber war

**Title**
> Phishing in a cyber war

**Category**
> ANALYSIS

**Difficulty**
> Easy

**Points**
> 120

**Description**
> A malicious actor is conducting social engineering attacks against Ukrainian officials. It also has targeted other countries around the region in the past. We are given some examples of domains it uses for phishing: ron-mil-pl[.]space ua-login[.]site passport-yandex[.]ru Can you give us more information? Q1 What is the code name for the group used by Mandiant and FireEye for reporting? (All upper case) Q2 Which country is this group based in? (Capitalized) Q3 What are the two domains used in the February attacks against Ukraine, as published by Ukrainian officials? (all lower case, with no []s) Flag format: FLAG{CODENAME_Country_domain.number.one_domain.number.two}

**Attachments**
> None

## Solution
https://www.fireeye.com/content/dam/fireeye-www/blog/pdfs/unc1151-ghostwriter-update-report.pdf
Q1:
UNC1151

https://securityaffairs.co/wordpress/128397/apt/belarusian-unc1151-targets-ukraine.html
Q2:
Belarus

https://www.proofpoint.com/us/blog/threat-insight/asylum-ambuscade-state-actor-uses-compromised-private-ukrainian-military-emails
Q3:
i.ua-passport.space
id.bigmir.space

## Flag
FLAG{UNC1151_Belarus_i.ua-passport.space_id.bigmir.space}
