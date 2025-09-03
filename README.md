# ISO 27001 Compliant Incident Management Report
<!-- hide -->

> By [@rosinni](https://github.com/rosinni) and [other contributors](https://github.com/4GeeksAcademy/deploying-wordpress-debian/graphs/contributors) at [4Geeks Academy](https://4geeksacademy.co/)

[![build by developers](https://img.shields.io/badge/build_by-Developers-blue)](https://4geeks.com)
[![build by developers](https://img.shields.io/twitter/follow/4geeksacademy?style=social&logo=twitter)](https://twitter.com/4geeksacademy)

*Estas instrucciones están [disponibles en español](https://github.com/breatheco-de/incident-report-management-exercise-project/blob/main/README.es.md)*
<!-- endhide -->

<!-- hide -->

### Before Starting...

> We need you! These exercises are created and maintained in collaboration with people like you. If you find any errors or typos, please contribute and/or report them.

<!-- endhide -->

## 📋 Project Purpose

This exercise aims to teach students how to identify and report an SQL injection vulnerability using the Damn Vulnerable Web Application (DVWA). The report should be made according to ISO 27001 standards for information security incident management.

**Learning Objectives:**
- Understand SQL injection vulnerabilities
- Learn to use DVWA for security testing
- Practice creating ISO 27001 compliant incident reports
- Gain hands-on experience with cybersecurity tools

## 🛠️ Technologies Used

- **Virtualization:** VirtualBox
- **Operating System:** Debian Linux
- **Web Server Stack:** LAMP (Linux, Apache, MySQL/MariaDB, PHP)
- **Vulnerable Application:** DVWA (Damn Vulnerable Web Application)
- **Database:** MySQL/MariaDB
- **Security Standards:** ISO 27001
- **Languages:** SQL, PHP, HTML
- **Tools:** Command Line, Web Browser

## 🌱 How to Install and Execute

### Requirements

- VirtualBox installed on your computer.
- A Debian virtual machine installed in VirtualBox. (We will use the machine previously configured in earlier classes).

#### Benefits of Using a Virtual Machine

- **Isolation:** Keeps the testing environment separate from your main operating system, protecting it from potential damage.
- **Ease of Restoration:** You can create snapshots of your virtual machine and easily restore them if something goes wrong.
- **Portability:** You can easily move and share the virtual machine with others.

## 📝 Instructions

* Open this URL and fork the repository https://github.com/breatheco-de/incident-report-for-sql-injection-exercise-project

 ![fork button](https://github.com/4GeeksAcademy/4GeeksAcademy/blob/master/site/src/static/fork_button.png?raw=true)

A new repository will be created in your account.

* Clone the newly created repository into your localhost computer.
* Once you have cloned successfully, follow the steps below carefully, one by one.


### Step 1: Verify the Virtual Machine Setup Before Starting

- [ ] In the "Network" section, select "Bridge Adapter" so the VM is on the same network as your host.
- [ ] Verify the correct installation of MySQL (MariaDB), Apache, and PHP (LAMP Stack).
- [ ] Set the root password for MariaDB and configure the basic security.

### Step 2: Installing and Configuring DVWA

- [ ] Download DVWA from the provided link:
    ```sh
    cd /var/www/html
    sudo apt-get install wget unzip
    sudo wget https://storage.googleapis.com/breathecode/virtualbox/DVWA.zip
    sudo unzip DVWA.zip
    sudo mv DVWA-master DVWA
    ```

- [ ] Configure DVWA
Change to the DVWA directory and rename the configuration file
```sh
cd DVWA/config 
sudo cp config.inc.php.dist config.inc.php
```
- [ ] Edit the `config.inc.php` file to set the MariaDB credentials:
```ssh
sudo nano config.inc.php
```
> 💡 IMPORTANT: Ensure the following lines have the correct credentials:
* $_DVWA[ 'db_user' ] = 'root';
* $_DVWA[ 'db_password' ] = 'root_password'; 
* $_DVWA[ 'db_database' ] = 'dvwa';

- [ ] Configure the Database
Log in to MariaDB and create the DVWA database
```sh
sudo mysql -u root -p 
CREATE DATABASE dvwa; 
EXIT;
```
- [ ] Adjust Permissions
```sh
sudo chown -R www-data:www-data /var/www/html/DVWA/
sudo chmod -R 755 /var/www/html/DVWA/
```
- [ ] Open a browser in your VM and go to http://localhost/DVWA/setup.php
- [ ] Review the setup and click "Create / Reset Database".


### Step 3: Conduct the SQL Injection Attack.
- [ ] Open a browser in the VM and go to http://localhost/DVWA.
- [ ] Log in to DVWA:
```
*Username: admin
*Password: password
```
- [ ] Set the Security Level
Go to the "DVWA Security" tab and select the "Low" security level to facilitate exploitation.

- [ ] Execute the SQL Injection
Go to the "SQL Injection" section in DVWA
Enter a simple SQL injection attack in the provided "User ID" field, for example:
```sh
1' OR '1'='1
```
Click "Submit" and observe how DVWA processes the injection and displays the database results.
> 💡 NOTE: You should see a list of all users extracted from the database, indicating a successful SQL injection.

![vulnerability](https://github.com/breatheco-de/incident-report-for-sql-injection-exercise-project/blob/main/assets/vulnerability.png?raw=true)


### Step 4: Incident Report.

- [ ] Follow the Report Structure
  * Report Title
  * Introduction
  * Incident Description
  * Reproduction Process
  * Incident Impact
  * Recommendations
  * Conclusion

> 💡 NOTE: Incident reports according to ISO 27001 standards do not specifically require the inclusion of images unless they are necessary to illustrate critical points or specific technical details of the incident. However, in most cases, reports often include screenshots, charts, or diagrams only if they are relevant to support the explanation of the incident or to demonstrate how the vulnerability exploitation was carried out.

[Download an example of an incident report](https://github.com/breatheco-de/incident-report-for-sql-injection-exercise-project/blob/main/assets/incident_ISO27001_report.pdf?raw=true)

## 📝 Delivery

* At the root of the forked project, upload the report in `.pdf` format with the name `incident-report.pdf`
