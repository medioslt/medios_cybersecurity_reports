## Unblocking a Falsely Blocked Website for a Client

**Incident Date:** July 28, 2023, 05:38:13 +1000 to July 28, 2023, 05:47:46 +1000
**Resolution Date:** August 8, 2023
**Prepared by:** Marius, SOC Analyst, medios.lt

### Introduction

Greetings,

I, Marius, a SOC Analyst from medios.lt, present this report detailing a case involving a client's website that was erroneously flagged for malware infection. The incident took place within a specified timeframe and required a comprehensive analysis to determine the root cause. This report outlines the investigative actions, findings, and recommended measures taken to address and resolve the issue.

### Investigative Actions

The following actions were undertaken as part of the analysis:

1. **FTP File Retrieval:** Downloaded the website files via FTP for examination.
2. **Comprehensive Scanning:** Utilized THOR Scanner, Thor Scanner, and additional YARA rules to scrutinize the website files. The goal was to identify signatures and evaluate the presence of potentially harmful content in content management system files. This resulted in false positives that were actually content management system files.
3. **ClamAV Scan:** Conducted a scan using the ClamAV free version, resulting in the absence of any malicious files.
4. **File Validation:** Verified the flagged incident by examining the specific log file:
   - Identified suspicious scanning activity originating from IP address 20.225.167.90 on July 28, 2023, within the time range of [July 28, 2023, 05:38:13 +1000] to [July 28, 2023, 05:47:46 +1000].
   - Validated the IP address against https://www.abuseipdb.com/check/20.225.167.90, confirming its association with a known web attack IP address.

### Log File Analysis

1. **YARAify Scan with ClamAV Filter:** Employed https://yaraify.abuse.ch/ to scan log files using the ClamAV filter, reproducing the same error.
2. **False-Positive Identification:** Discovered instances of false-positive triggers within the log entries:
   ```
   20.225.167.90 - - [28/Jul/2023:05:41:30 +1000] "GET /en/indoxploit.php HTTP/1.1" 302 0 "" "Go-http-client/1.1" ""
   20.225.167.90 - - [28/Jul/2023:05:41:32 +1000] "GET /en/indoxploit.php HTTP/2.0" 404 0 "http://clientsite.com//IndoXploit.php" "Go-http-client/2.0" ""
   ```
   The ClamAV filter incorrectly triggered due to these specific entries, which referenced "indoxploit.php."

### Root Cause Analysis

The core issue stems from a rule misalignment with the actual website system. The rule's inappropriate detection of "indoxploit.php" is incongruent with the customized content management system utilized by the website. Consequently, the rule's flagging of these entries as suspicious is unwarranted.

### Recommendations

To address the situation effectively, the following recommendations are suggested:

1. **Website Unblock:** Swiftly unblock the affected website to restore its normal functionality.
2. **ClamAV Signature Review:** Conduct an in-depth review and refinement of the ClamAV signature to eliminate false positives stemming from log files.
3. **Firewall Enhancement:** Enhance the firewall's effectiveness to counter automated scanning tools, especially those deployed by IP address 20.225.167.90.

### Conclusion

In summary, I, Marius, a SOC Analyst at medios.lt, confirm that the reported antivirus error stemmed from a false positive trigger in the ClamAV signature. The proposed measures aim to address the issue, optimize the signature accuracy, and reinforce the firewall against similar occurrences. For further assistance or inquiries, please feel free to contact us.

Best regards,

Marius
SOC Analyst
medios.lt
