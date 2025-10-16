# 🧱 Linux LAMP + Node.js Local Development Setup (Auto Install Version)

A simple, beginner-friendly guide to install and configure a **LAMP stack (Linux, Apache, MySQL, PHP)** and **Node.js (multiple versions via NVM)** for local full-stack development.

All commands below use **`-y` (yes)** for auto-confirmation — just copy, paste, and run.

> ⚠️ Default MySQL and phpMyAdmin password: `1`  
> (You can change it anytime later.)

---

## ⚙️ What You’ll Get

- Apache Web Server  
- PHP (with all common extensions)  
- MySQL Database Server  
- phpMyAdmin (web UI for MySQL)  
- Node.js (with multiple versions managed by NVM)

---

## 🧩 Step-by-Step Installation Guide

### 1. Update System
```bash
sudo apt update -y && sudo apt upgrade -y
```

---

### 2. Install Apache
```bash
sudo apt install apache2 -y
sudo systemctl enable apache2
sudo systemctl start apache2
```

Test in browser:  
👉 [http://localhost](http://localhost)

You should see the Apache default page.

---

### 3. Install PHP and Extensions
```bash
sudo apt install -y php libapache2-mod-php php-mysql php-cli php-curl php-xml php-mbstring php-zip php-gd php-intl unzip
```

Check version:
```bash
php -v
```

Restart Apache:
```bash
sudo systemctl restart apache2
```

---

### 4. Install MySQL (Password = `1`)
```bash
sudo apt install mysql-server -y
sudo systemctl enable mysql
sudo systemctl start mysql
```

Set root password:
```bash
sudo mysql -e "ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '1'; FLUSH PRIVILEGES;"
```

Test:
```bash
mysql -u root -p
# password: 1
```

---

### 5. Install phpMyAdmin (Password = `1`)
```bash
echo "phpmyadmin phpmyadmin/dbconfig-install boolean true" | sudo debconf-set-selections
echo "phpmyadmin phpmyadmin/app-password-confirm password 1" | sudo debconf-set-selections
echo "phpmyadmin phpmyadmin/mysql/admin-pass password 1" | sudo debconf-set-selections
echo "phpmyadmin phpmyadmin/mysql/app-pass password 1" | sudo debconf-set-selections
echo "phpmyadmin phpmyadmin/reconfigure-webserver multiselect apache2" | sudo debconf-set-selections
sudo apt install -y phpmyadmin
```

Link phpMyAdmin to Apache:
```bash
sudo ln -s /usr/share/phpmyadmin /var/www/html/phpmyadmin
sudo systemctl restart apache2
```

Access in browser:  
👉 [http://localhost/phpmyadmin](http://localhost/phpmyadmin)  
**Username:** root  
**Password:** 1

---

### 6. (Optional) Set Permissions for Web Directory
```bash
sudo chown -R $USER:www-data /var/www/html
sudo chmod -R 755 /var/www/html
```

---

### 7. Install Node.js (with NVM for Multiple Versions)
Install NVM:
```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/master/install.sh | bash
source ~/.bashrc
```

Verify NVM:
```bash
nvm -v
```

Install Node versions:
```bash
nvm install 18
nvm install 20
```

Set default Node:
```bash
nvm alias default 20
```

Switch between versions:
```bash
nvm use 18
```

Check versions:
```bash
node -v
npm -v
```

---

## ✅ Verification Summary

| Component | Command / URL | Password |
|------------|----------------|-----------|
| Apache | [http://localhost](http://localhost) | — |
| PHP | `php -v` | — |
| MySQL | `mysql -u root -p` | `1` |
| phpMyAdmin | [http://localhost/phpmyadmin](http://localhost/phpmyadmin) | `root / 1` |
| Node.js | `node -v` | — |
| NPM | `npm -v` | — |

---

## 🐳 Optional: Docker Setup
If you prefer using containers, you can use Docker to run:
- PHP + Apache
- MySQL
- phpMyAdmin
- Node.js

Ask ChatGPT to generate a `docker-compose.yml` file for this exact setup.

---

## 💡 Tips

- To change MySQL password later:
  ```bash
  sudo mysql -e "ALTER USER 'root'@'localhost' IDENTIFIED BY 'your_new_password'; FLUSH PRIVILEGES;"
  ```
- Place your PHP projects inside:
  ```
  /var/www/html/your_project/
  ```

---

## 🧑‍💻 Author

**Md. Mahajurul Karim (Maha)**  
Senior Software Engineer | PHP, Python, React.js, DevOps-Aware  
📧 mahajur77@gmail.com  
🌐 [LinkedIn](https://linkedin.com/in/maha-karim) | [GitHub](https://github.com/inversemaha)

---

## 📝 License

This guide is open-source under the [MIT License](LICENSE).  
You are free to use, modify, and share it.

---

### ⭐ Support
If this helped you, star the repo and share it with your dev friends 😊
