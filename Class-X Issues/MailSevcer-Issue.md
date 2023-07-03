# Mail Server Misconfiguration
## Email spoofing can happend due
- SPF record not set for the particular email
- Missing of DMARC protocol for the particular email

## What is a SPF Record ?
 “Sender Policy Framework”. It is a type of Domain Name System (DNS) record that can help to prevent email address forgery or email spoofing.
## What is a DMARC Protocol ?
DMARC stands for “Domain-based Message Authentication, Reporting & Conformance” is a protocol that uses Sender Policy Framework, (SPF) and Domain-Keys identified mail (DKIM) to determine the authenticity of an email message.

## If it is misconfigured email can be spoofed
- Go to your target company and collect all the possible emails of that company
- Use gau/waybackurl etc. Hunter.io
- [Now check the SPF and DMARC record of all the emails :](https://mxtoolbox.com/)
- Now if you get an email (xyz@company.com), then go for its exploitation
- Visit https://emkei.cz/ in order to exploit the issue
- Here you’ll need to fill From-email, To and Subject
- in From-email add the company’s email and in To add your own email and in Subject you can add anything (like Hacking You, Bounty Time etc.)
- Check your inbox and you’ll get the email from that company which was sent by you

- [Mail Sender](https://anonymailer.net/)
