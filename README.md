# Deploy Apache+PHP5+MySQL in Windows7 Pro
### 1. Author：HHX
### 2. Version：v1.0.0
### 3. Date：2014-11-19

### configuring this computer to become：
#### operating system：Windows7 Pro
#### cpu：Intel(R) Core(TM) i7 CPU    M620 @ 2.6.7GHz
#### RAM：4G
#### system type：A 64 bit operating system 

## 一、 Deploy Apache2.4.7 (httpd-2.4.7-win64-VC11.zip)：
### 1. Extract the installation package：httpd-2.4.7-win64-VC11.zip and put on their installation directory.For example: D:\Apache.
### 2. Then the httpd.conf (D:\Apache\Apache24\conf) configuration file modification.
#### a) The root path to modify the ServerRoot Apache:(ROW:37)ServerRoot "c:/Apache24"  change-->ServerRoot "D/Apache/Apache24".
#### b) Modify the ServerName of your host name:(ROW：217)ServerName www.example.com:80,The front of the # removed, this property needed to start Apache from the command line in the.
#### c) Modify the DocumentRoot Apache visit access to the main folder directory, is php、html code file location.The Apache default path in the htdoce(D:\Apache\Apache24\htdoce),there will be a simple entrance file index.html.This path can be to change it yourself, I'm here to configure it in my own new folder www(E:\www):(ROW:242)DocumentRoot "c:/Apche24/htdocs"  <Directory "c:/Apache24/htdoce">  change-->DocumentRoot "E:/www"  <Directory "E:\www">
#### d) Modify the entrance file's deploy:DirectoryIndex,just like situation we use index.php、index.html、index.htm as the entrance of the web project.The Apache default entrance only index.php,need to add two other support.Of course, this text study the entrance set up root can sit self demand add and subtract, deductible ratio more strictly economical request can only give to copy index.php,so this entrance on the project as it is index.php(ROW:275)<IfModuledir_module>  DirectoryIndexindex.html  </IfModule>  change-->       <IfModuledir_module>  DirectoryIndex index.php index.htm index.html  </IfModule>
#### e) Set the serverscript directory:(ROW:359)ScriptAlias/cgi-bin/ "c:/Apache24/cgi-bin/"  change--> ScriptAlias/cgi-bin/ "D:/Apache/Apache24/cgi-bin"
#### f) (ROW:374)<Directory"c:/Apache24/cgi-bin">  AllowOverride None  Options None  Require all granted  </Directory>  change-->  <Directory"D:/Apache/Apache24/cgi-bin">          AllowOverride None  Options None  Require all granted  </Directory>
### 3. Then you can start Apache:start--run--cmd,open command.Then enter the D:\phpEnv\Apache24\bin directory enter,httpd enter.As shown in Fig:
![](https://raw.githubusercontent.com/hhx1109/MagentoInstall/master/646D%5BNXH~DLL2%7B4%5DIB%5BDBQG.jpg)
Put D:\Apache\Apache24\htdocs the index.php directory into the E:\www directory.use browser sivit it there will be "It works",it means that the apache is correctly installed and started.As shown in Fig:
![](https://raw.githubusercontent.com/hhx1109/MagentoInstall/master/X(DME6AAM87S$%5BHEI%5B@J%5DUH.png)
### 4. Apache will be added to the window service startup items inside and set the boot:
#### a) First close the httpd service (the command window is closed);
#### b) Re open a new command window and get into D:\Apache\Apache24\bin directory,add the HTTP service command is:
```
    httpd.exe -kinstall -n "serviceName"
```
#### serviceName is service's name.After the success will appear below the picture:
![](https://raw.githubusercontent.com/hhx1109/MagentoInstall/master/UL%5DM6$WD4%5BE1H5%25VAR0I~3W.jpg),
"Errors reported here must be corrected before the service can be started",is not error,not wrong but prompt you if this line appear below the mistake error after activation solution!
### If appear error message failed to open the winNT service manager,set control panel-->user accounts and family safety-->user accounts-->change user account control settings notice for never notice,restart the computer.
#### This time you can see the Apache24 service in the window service startup,as shown in Fig:
![](https://raw.githubusercontent.com/hhx1109/MagentoInstall/master/@K1%60ENIB15A%7BRFU%5DPD~2ERG.jpg)
#### click start on it,as shown in Fig:![](https://raw.githubusercontent.com/hhx1109/MagentoInstall/master/@K1%60ENIB15A%7BRFU%5DPD~2ERG.jpg)
## 二、 Install and Deploy PHP5.5.10 (php-5.5.10-Win32-VC11-x64.zip):
### 1. Download php-5.5.10-Win32-VC11-x64.zip extract to the installation directory.My directory is (D:\php).
### 2. The directory of the php.ini-development file copy and rename the php.ini he is PHP configuration file.
### 3. Add PHP support for Apache services,Apache http.conf configuration file opens in the final plus:
```
    # php5 support
      LoadModule php5_module D:/php/php5apache2_4.dll
      AddType application/x-httpd-php .php .html .htm
    # configure thepath to php.ini
      PHPIniDir "E:/www"
```
#### ! Add the LoadModule php5apache2_4.dll to ensure that exist in the PHP folder
### 4. Restart the Apache server.
### 5. checkout:
#### a) Delete other files in www;
#### b) Add a new index.php file,the content is "<?php phpinfo(); ?>" and save;
#### c) Set D:\php\php.ini date.timezone:Asia/Shanghai;
#### d) Access PHP information means that PHP has been successfully installed
### Pay attention to: When the below situation, please enter the management-->service, the resumption of the apacheService can be solved!
![](https://raw.githubusercontent.com/hhx1109/MagentoInstall/master/NVN)79X~%5DB3M41TEIVB0UJF.jpg)
## 三、 Install the MySQL management tools (navicat091_lite_cs.exe):
### 1. Download Navicat;
### 2. Install the Navicat;
### 3. Run this procedure;
### 4. Click connection,chooce mysql;
### 5. Enter install MySQL's userName and passWord.
### ! This tool can also execute a SQL statement.
## 四、 Install MySQL5.6.10 (MySQL_5.6.10_winx64):
### 1. 