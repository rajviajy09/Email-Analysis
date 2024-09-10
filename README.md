# Email Analysis Project

## Overview

This project focuses on analyzing email content for potential threats, such as phishing or malicious attachments. The analysis covers key elements such as email headers, attachments, sender details, and embedded links. **CyberChef** and **VMware** were used for decoding and safely analyzing the content.

## Scenario

In a fictional scenario, a country faces a crisis due to citizen abduction and receives a ransom demand via email. The email threatens harm unless a ransom of **1 billion candies** is paid, with instructions pointing to a suspicious attachment.

## Email Analysis Breakdown

### 1. Email Headers

Email headers are critical for understanding the sender’s legitimacy. Here’s what we found:

- **ARC Header (Authenticated Received Chain):**  
  Used for verification purposes. A trusted intermediate server digitally signs the header.  
  *Suspicious detail:* A forged ARC header was detected, potentially faked by a malicious sender.
  
  _**[Insert ARC Header Image Here]**_

- **Return Path:**  
  The return path is an email address used if the email fails to send.  
  *Suspicious detail:* The return path didn’t match the sender’s domain, hinting at phishing.

  _**[Insert Return Path Image Here]**_

- **Authentication Results (SPF, DKIM, DMARC):**  
  These show email authenticity protections.
  
  - **SPF (Sender Policy Framework):**  
    The domain `microapple.com` failed SPF validation, indicating that the mail server (IP `93.99.104.210`) was not authorized to send emails for the domain.  
    *Suspicious detail:* SPF failure signals that the email may have originated from an illegitimate source.
    
    _**[Insert SPF Failure Image Here]**_

### 2. Sender and Receiver Info

*Suspicious detail:* Discrepancies were found between the "Sender" and "Reply-to" email addresses, which is a common tactic used in phishing attacks.



### 3. Message ID

Each email has a unique message ID. This one was present but didn’t follow standard patterns for the sending domain, further raising suspicion.

_**[Insert Message ID Image Here]**_

### 4. Encoding Type and Content

The email content uses a specific encoding type. In this case, Base64 encoding was detected. This can often conceal malicious payloads.

_**[Insert Encoding Type Image Here]**_

## Step-by-Step Process for Analyzing Base64 Encoded Attachments

1. **Decode Base64 to Binary:**  
   Using **CyberChef**, we decoded the Base64-encoded attachment back into its original binary format.
   
2. **Convert Binary to Hex:**  
   The binary data was converted into hexadecimal using **CyberChef**. This step makes the data easier to analyze.

3. **Identify File Signature:**  
   We analyzed the hexadecimal string to identify the file type using the first few bytes (magic numbers).

   *Suspicious detail:* The file was labeled as a **PDF**, but after analysis, it was revealed to be a **ZIP file** (`50 4b 03 04`).

_**[Insert Hex Signature Image Here]**_

---

### File Type Analysis Results:

- **DaughterCrown:**  
  First bytes `ff d8 ff e0 00 10`, identified as a **JPEG** image.
  
  *Suspicious detail:* The file type didn’t match its claimed format in the email.
  
- **GoodJobMajor:**  
  First bytes `25 50 44 46`, identified as a **PDF** document.

  *Suspicious detail:* It was correctly labeled, but further inspection is required to ensure no hidden threats.

- **Money.xlsx:**  
  Initially appears as an Excel file. However, we verified the extension and header to confirm its legitimacy.

---

### Conclusion

This project highlights how important it is to inspect every detail in an email, from headers to file attachments. In this case, we found multiple suspicious indicators, such as mismatched domains, SPF failures, and incorrectly labeled files, which pointed to potential phishing attempts.

---

### How to Use

1. Clone this repository.
2. Analyze suspicious emails by decoding their headers and attachments.
3. Use **CyberChef** for Base64 decoding and file signature identification.
4. Analyze files in **VMware** to prevent accidental execution of malicious content.

---

### Tools Used
- **CyberChef**: For Base64 decoding and file analysis.
- **VMware**: To create a safe virtual environment for testing.

### Future Improvements

- Automate parts of the analysis to quickly detect phishing patterns.
- Expand the project to analyze email attachments for malware signatures.
