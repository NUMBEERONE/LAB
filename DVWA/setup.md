# DVWA Setup on Kali Linux (WSL)

## 1. Web Server Installation & Start

**Action:** Installed and started Apache2 web server.

**Commands:**
sudo apt install apache2  
sudo service apache2 start  

**Result:**
- Apache is running
- PHP files can be accessed from `/var/www/html/dvwa`
- DVWA loads in browser via `http://localhost/dvwa`

---

## 2. Database Server Setup

**Action:** Installed and started MariaDB.

**Commands:**
sudo apt install mariadb-server  
sudo service mariadb start  

**Result:**
- Database service is active
- Used for DVWA data storage (users, vulnerabilities)

---

## 3. PHP Environment Configuration

**Action:** Installed PHP and MySQL connector.

**Commands:**
sudo apt install libapache2-mod-php php-mysql  
sudo a2enmod php8.2  

**Result:**
- Apache can process PHP files
- Fixes issue where raw PHP code is displayed

---

## 4. DVWA Configuration File

**Action:** Created and configured DVWA config file.

**File Path:**
/var/www/html/dvwa/config/config.inc.php  

**Key Settings:**
$_DVWA['db_user'] = 'root';  
$_DVWA['db_password'] = '';  

**Result:**
- DVWA connected to local database

---

## 5. Database Authentication Fix (HTTP 500 Error)

**Problem:**
- MariaDB uses `unix_socket` authentication by default
- DVWA requires password-based authentication

**Solution (run inside MySQL):**
ALTER USER 'root'@'localhost' IDENTIFIED VIA mysql_native_password USING PASSWORD('');  

**Result:**
- HTTP 500 error resolved
- PHP can authenticate with database

---

## 6. Final Initialization

**URL:**
http://localhost/dvwa/setup.php  

**Action:**
- Click "Create / Reset Database"

**Result:**
- Tables created
- Default data inserted
- DVWA ready for login

---

## 7. Default Credentials

Username: admin  
Password: password  

---

## Verification Checklist

- [ ] Apache running  
- [ ] MariaDB running  
- [ ] PHP working correctly  
- [ ] DVWA config set  
- [ ] Database initialized  
- [ ] Login successful  

---

## Notes

- Setup uses intentionally weak security:
  - Empty root password
  - Root database access from web app
- Suitable for:
  - SQL Injection testing
  - XSS practice
  - Web vulnerability labs

**Do not use in production environments**
