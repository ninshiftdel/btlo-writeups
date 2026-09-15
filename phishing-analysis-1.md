# Phishing Analysis 1

## Scenario

A user forwarded a suspicious email to the SOC. It looked like a harmless bounce-back message, but the original phishing email was actually attached inside it. The attacker spoofed a dead mailbox, and when the bounce came back to the spoofed sender, the phishing payload landed in the victim's inbox.

## Investigation Steps

- Opened the `.eml` file in Notepad to inspect raw headers.
- Traced the `Received:` chain to find the originating IP.
- Ran reverse DNS via WHOIS/DomainTools to identify the sending host.
- Extracted the attached email and analyzed its HTML body.
- Cleaned up the URL (broken by `=3D` encoding) and confirmed the hosting platform.
- Used URL2PNG to view the malicious page (already taken down).

## Findings

Question | Answer
- Primary recipient | `kinnar1975@yahoo.co.uk`
- Subject | `Undeliverable: Website contact form submission`
- Date sent | `Thu, 18 Mar 2021 15:13:56 +1100`
- Originating IP | `103.9.171.10`
- Reverse DNS host | `c5s2-1e-syd.hosting-services.net.au`
- Attached file | `Website contact form submission.eml`
- Malicious URL | `hxxps://35000usdperwwekpodf.blogspot[.]sg?p=9swghttps://35000usdperwwekpodf.blogspot[.]co[.]il?o=0hnd`
- Hosting service | Blogspot
- Page heading | `Blog has been removed`

## Indicators of Compromise

Type | Indicator
- IP | `103.9.171.10`
- Host | `c5s2-1e-syd.hosting-services.net.au`
- URL | `hxxps://35000usdperwwekpodf.blogspot[.]sg`
- URL | `hxxps://35000usdperwwekpodf.blogspot[.]co[.]il`
- Email | `kinnar1975@yahoo.co.uk`

## MITRE ATT&CK

- Initial Access → T1566.002 — Phishing: Spearphishing Link

## Recommendations

- Block originating IP and both Blogspot URLs at email gateway and web proxy.
- Report the Blogspot pages to Google for takedown.
- Remind users not to interact with unexpected bounce messages.

## Conclusion

True positive. No credentials were entered, so the incident was contained cleanly.
