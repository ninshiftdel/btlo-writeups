# Phishing Analysis 2

## Scenario

A user received an email impersonating Amazon, claiming their account had been locked and needed verification within 72 hours. Classic urgency play. During investigation, the attacker's own Facebook profile URL was found hidden in the email footer.

## Investigation Steps

- Opened the `.eml` file in Notepad to inspect raw headers.
- Identified spoofed sender domain, recipient, and originating IP.
- Decoded the Base64-encoded HTML body using Base64decode.
- Extracted the main call-to-action URL and analyzed it with URL2PNG.
- Found a Facebook profile URL in the email footer — OPSEC failure by the attacker.

## Findings

Question | Answer
- Sending address | `amazon@zyevantoby.cn`
- Recipient | `saintington73@outlook.com`
- Subject | `Your Account has been locked`
- Imitated company | Amazon
- Date sent (raw) | `Wed, 14 Jul 2021 01:40:32 +0900`
- Main CTA URL | `hxxps://amazo.zzuyuchengzhika[.]cn/?mailtoken=saintington73@outlook.com`
- Page heading | `Account locked`
- Body encoding | `base64`
- Logo URL | `images.squarespace-cdn.com/.../amazon-logo`
- Facebook username | `amir.boyka.7`

## Indicators of Compromise

Type | Indicator
- Email | `amazon@zyevantoby.cn`
- Domain | `zyevantoby.cn`
- URL | `hxxps://amazo.zzuyuchengzhika[.]cn`
- IP | `45.156.23.138`
- Social | `facebook.com/amir.boyka.7`

## MITRE ATT&CK

- Initial Access → T1566.002 — Phishing: Spearphishing Link
- Resource Development → T1585.001 — Establish Accounts: Social Media Accounts

## Recommendations

- Block sender domain, malicious URL, and originating IP.
- Escalate Facebook profile to Meta and law enforcement.
- Coach users on urgency cues and verifying sender domains.

## Conclusion

True positive. The attacker's OPSEC failure provided a strong attribution lead. No credentials were compromised.
