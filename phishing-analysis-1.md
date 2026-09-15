# Phishing Analysis — Website Contact Form Submission

- **Platform:** Blue Team Labs Online (BTLO)
- **Category:** Security Operations
- **Difficulty:** Easy
- **Date Completed:** [Insert Date]
- **Verdict:** True Positive

## 1. Executive Summary
A user received a suspicious email disguised as a bounce-back notice for a website contact form submission. The email contained the original phishing message as an attachment. Investigation of the raw headers and decoded body revealed a credential-harvesting attempt hosted on Blogspot. IOCs were extracted and remediation steps were documented.

## 2. Investigation Steps
1. Opened the `.eml` file in Notepad to inspect the raw email headers.
2. Identified the originating IP from the first `Received:` header in the chain.
3. Performed reverse DNS via WHOIS to identify the sending infrastructure.
4. Extracted the embedded attachment and analyzed the HTML body of the original email.
5. Decoded the malicious URL and confirmed the hosting platform.

## 3. Answers to Challenge Questions
| Question | Answer |

| Primary recipient | `kinnar1975@yahoo.co.uk` |
| Subject | `Undeliverable: Website contact form submission` |
| Date and time sent | `Thu, 18 Mar 2021 15:13:56 +1100` |
| Originating IP | `103.9.171.10` |
| Reverse DNS host | `c5s2-1e-syd.hosting-services.net.au` |
| Attached file name | `Website contact form submission.eml` |
| URL inside attachment | `https://35000usdperwwekpodf.blogspot.sg?p=9swghttps://35000usdperwwekpodf.blogspot.co.il?o=0hnd` |
| Webpage hosting service | `Blogspot` |
| Heading text (URL2PNG) | `Blog has been removed` |

## 4. Indicators of Compromise (IOCs)
| Type | Indicator | Description |

| IP | `103.9.171.10` | Originating IP of attacker |
| Email | `kinnar1975@yahoo.co.uk` | Spoofed primary recipient |
| URL | `hxxps://35000usdperwwekpodf.blogspot[.]sg` | Phishing redirect link |
| URL | `hxxps://35000usdperwwekpodf.blogspot[.]co[.]il` | Credential harvesting page |
| Domain | `blogspot.sg`, `blogspot.co.il` | Free hosting abused for phishing |
| Host | `c5s2-1e-syd.hosting-services.net.au` | Attacker's sending server |

## 5. MITRE ATT&CK Mapping
- **Tactic:** Initial Access
- **Technique:** T1566.002 — Phishing: Spearphishing Link

## 6. Recommendations
- Block the originating IP `103.9.171.10` at the email gateway and firewall.
- Block the malicious URLs and Blogspot domains at the web proxy.
- Educate the user on identifying spoofed sender addresses and unsolicited contact form submissions.
- Report the malicious Blogspot pages to Google for takedown.

## 7. Conclusion
The email was a **True Positive** phishing attempt. No credentials were submitted, and no compromise occurred.

