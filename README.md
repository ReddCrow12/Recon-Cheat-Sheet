# 🐛 מדריך מקיף לבאג באונטי (Bug Bounty) 🐛

## 📋 תוכן עניינים
- [מבוא](#מבוא)
- [כלים חיוניים](#כלים-חיוניים)
- [שיטות ריקון](#שיטות-ריקון)
- [רשימת בדיקות](#רשימת-בדיקות)
- [מציאת מטרות למתחילים](#מציאת-מטרות-למתחילים)
- [סוגי פגיעויות נפוצות](#סוגי-פגיעויות-נפוצות)
- [פקודות מומלצות לכלים](#פקודות-מומלצות-לכלים)

## מבוא
מדריך זה נועד לספק מידע מקיף על כלים, שיטות וטכניקות לבאג באונטי. המדריך מתאים למתחילים ומתקדמים כאחד.

## כלים חיוניים

### 🛠️ כלי סריקה ומיפוי
- **Nmap** - סריקת פורטים וזיהוי שירותים
- **Subfinder** - איתור תתי-דומיינים
- **Katana** - סריקת תתי-דומיינים מתקדמת
- **Waybackurls** - איתור URL-ים היסטוריים
- **FFuf** - סריקת תתי-דומיינים ופורצים
- **Nuclei** - סריקת פגיעויות אוטומטית
- **WPScan** - סריקת אתרי WordPress
- **SQLMap** - זיהוי וניצול פגיעויות SQL Injection

### 🔍 כלי DNS
- **Dig** - שאילתות DNS מתקדמות
- **Whois** - מידע על רישום דומיינים
- **DNSRecon** - מיפוי DNS מקיף

## שיטות ריקון

### שלב 1: איסוף מידע
1. איתור תתי-דומיינים
2. איסוף IP-ים
3. סריקת פורטים
4. איתור טכנולוגיות
5. איתור נקודות כניסה

### שלב 2: מיפוי
1. מיפוי נקודות כניסה
2. זיהוי פונקציונליות
3. איתור פרמטרים
4. מיפוי API-ים

### שלב 3: בדיקות
1. בדיקות אוטומטיות
2. בדיקות ידניות
3. ניתוח קוד
4. בדיקות אבטחה

## רשימת בדיקות

### ✅ בדיקות בסיסיות
- [ ] סריקת תתי-דומיינים
- [ ] סריקת פורטים
- [ ] בדיקת SSL/TLS
- [ ] איתור טכנולוגיות
- [ ] בדיקת headers
- [ ] בדיקת cookies
- [ ] בדיקת CORS
- [ ] בדיקת CSP

### ✅ בדיקות מתקדמות
- [ ] בדיקות XSS
- [ ] בדיקות SQL Injection
- [ ] בדיקות SSRF
- [ ] בדיקות XXE
- [ ] בדיקות RCE
- [ ] בדיקות LFI/RFI
- [ ] בדיקות IDOR
- [ ] בדיקות CSRF

## מציאת מטרות למתחילים

### 🎯 המלצות למתחילים
1. התחילו בפלטפורמות כמו:
   - HackerOne
   - Bugcrowd
   - Synack
2. חפשו תוכניות עם:
   - דירוג קושי נמוך
   - תגמולים סבירים
   - תמיכה טובה
3. התמקדו בפגיעויות בסיסיות:
   - XSS
   - SQL Injection
   - CSRF
   - IDOR

## סוגי פגיעויות נפוצות

### 🔥 פגיעויות קריטיות
1. **Remote Code Execution (RCE)**
   - ניצול פגיעויות בקוד
   - ניצול פגיעויות בשרתים
   - ניצול פגיעויות באפליקציות

2. **SQL Injection**
   - הזרקת SQL
   - ניצול פרמטרים
   - ניצול טופסי חיפוש

3. **Cross-Site Scripting (XSS)**
   - XSS מוחזר
   - XSS מאוחסן
   - XSS מבוסס DOM

### 🎯 פגיעויות בינוניות
1. **Server-Side Request Forgery (SSRF)**
2. **XML External Entity (XXE)**
3. **Insecure Direct Object References (IDOR)**
4. **Cross-Site Request Forgery (CSRF)**

## פקודות מומלצות לכלים

### Nmap
```bash
# סריקה בסיסית
nmap -sV -sC -p- target.com

# סריקה אגרסיבית
nmap -A -T4 -p- target.com

# סריקת SSL
nmap -sV --script ssl-enum-ciphers -p 443 target.com

# סריקת פגיעויות
nmap --script vuln target.com
```

### Subfinder
```bash
# סריקה בסיסית
subfinder -d target.com -o subdomains.txt

# סריקה עם מקורות נוספים
subfinder -d target.com -sources all -o subdomains.txt

# סריקה עם DNS
subfinder -d target.com -recursive -o subdomains.txt
```

### Nuclei
```bash
# סריקה בסיסית
nuclei -u target.com

# סריקה עם תבניות ספציפיות
nuclei -u target.com -t cves/

# סריקה אגרסיבית
nuclei -u target.com -severity critical,high -c 50
```

### SQLMap
```bash
# בדיקת פרמטר
sqlmap -u "http://target.com/page.php?id=1"

# בדיקת טפסים
sqlmap -u "http://target.com/login.php" --forms

# בדיקה עם cookies
sqlmap -u "http://target.com/page.php" --cookie="PHPSESSID=123"
```

### FFuf
```bash
# סריקת תתי-דומיינים
ffuf -w wordlist.txt -u https://FUZZ.target.com

# סריקת תיקיות
ffuf -w wordlist.txt -u https://target.com/FUZZ

# סריקה עם headers
ffuf -w wordlist.txt -u https://target.com/FUZZ -H "Cookie: session=123"
```

### WPScan
```bash
# סריקה בסיסית
wpscan --url target.com

# סריקה אגרסיבית
wpscan --url target.com --enumerate p,t,u

# סריקה עם API
wpscan --url target.com --api-token YOUR_TOKEN
```

### Katana
```bash
# סריקה בסיסית
katana -u target.com

# סריקה עם פילטרים
katana -u target.com -f "\.(php|asp|aspx|jsp)$"

# סריקה עם headers
katana -u target.com -H "Cookie: session=123"
```

### Dig
```bash
# שאילתת A
dig target.com A

# שאילתת MX
dig target.com MX

# שאילתת TXT
dig target.com TXT

# שאילתת NS
dig target.com NS
```

### Waybackurls
```bash
# איתור URL-ים היסטוריים
waybackurls target.com > urls.txt

# איתור עם פילטרים
waybackurls target.com | grep "\.php"

# איתור עם פרמטרים
waybackurls target.com | grep "="
```

## 🎯 סימנים לזיהוי פגיעויות

### SQL Injection
- שגיאות SQL
- זמני תגובה שונים
- התנהגות לא צפויה
- הודעות שגיאה חשודות

### XSS
- קוד JavaScript מוחזר
- תגיות HTML מוחזרות
- פרמטרים המשקפים קלט
- אירועי JavaScript

### SSRF
- גישה לשירותים פנימיים
- שגיאות שרת
- תגובות לא צפויות
- גישה למידע רגיש

### XXE
- שגיאות XML
- גישה לקבצים
- תגובות לא צפויות
- שגיאות שרת

## 📝 טיפים חשובים

1. **תיעוד**
   - תיעדו כל שלב בתהליך
   - צלמו מסכים
   - שמרו לוגים
   - תיעדו PoC

2. **אתיקה**
   - אל תפגעו במערכות
   - אל תגנבו מידע
   - אל תפרו פרטיות
   - שמרו על סודיות

3. **למידה מתמדת**
   - עקבו אחרי עדכונים
   - קראו בלוגים
   - השתתפו בפורומים
   - למדו מקהילה

## 🔄 מתי לעבור לשלב הבא?

1. **סיימתם את כל הבדיקות הבסיסיות**
2. **לא מצאתם פגיעויות בסיסיות**
3. **הבנתם את המערכת לעומק**
4. **יש לכם PoC מוצלח**
5. **הפגיעות מאומתת ומתועדת**

## 📚 משאבים נוספים

### בלוגים מומלצים
- PortSwigger Web Security Blog
- OWASP
- HackerOne Blog
- Bugcrowd Blog

### קורסים מומלצים
- PortSwigger Web Security Academy
- OWASP WebGoat
- TryHackMe
- HackTheBox

### כלים נוספים
- Burp Suite
- OWASP ZAP
- Metasploit
- Acunetix
- Nessus

## ⚠️ אזהרה
מדריך זה נועד למטרות לימוד ומחקר בלבד. השימוש בכלים ובטכניקות המתוארות במדריך זה חייב להיות בהתאם לחוק ולאתיקה המקצועית. האחריות על השימוש בכלים ובטכניקות המתוארות במדריך זה היא על המשתמש בלבד.

---
*עדכון אחרון: 2024* 