[# AutoApiSecret](https://51.ruyo.net/15646.html

# AutoApiSecret-encrypted version

AutoApi series: AutoApi, AutoApiSecret, AutoApiSR, AutoApiS

### project instruction ###

* Use github action to realize **automatic calling of api** at regular intervals to keep E5 development active.
* **Free, no additional equipment/server required**, just forget it after deployment.
* Encrypted version, hides application ID + secret, protects account security.

### Special Instructions/Thanks ###

*Original tutorial blogger - Shady (Kuan ID-Paran): https://blog.432100.xyz/index.php/archives/50/

* Ordinary version address: https://github.com/wangziyingwen/AutoApi

* Encrypted version address (recommended): https://github.com/wangziyingwen/AutoApiSecret

* Imitate human application development version (including upgrade steps): https://github.com/wangziyingwen/AutoApiSR

* Super version address: https://github.com/wangziyingwen/AutoApiS

* **Common errors and solutions/update log**: https://github.com/wangziyingwen/Autoapi-test

* Get the refresh_token gadget from the web page (not recommended): https://github.com/wangziyingwen/GetAutoApiToken

* Video tutorial: (I operate very slowly, so I can double speed/fast forward by myself)

   * Online/download address: https://kino-onemanager.herokuapp.com/Video/AutoApi%E6%95%99%E7%A8%8B.mp4?preview

   * Station B: https://www.bilibili.com/video/av95688306/

     ​

    **The above recommendations/disrecommendations are just personal opinions, please choose the version yourself, and you can use it at the same time**.

-------------------------------------------------- ----------

### Steps ###



The first step is to register an application at https://portal.azure.com/#home. There are too many online tutorials for this step, so I won’t write it in detail. I will outline the process.
First log in to the website with the e5 administrator account, then find Azure Active Directory on the homepage and click on it. Then find the directory on the left and click Application Registration. Then click New Registration at the top and a new application interface will pop up. Fill in the application name as you like, and then Select an account in any organization directory (any Azure AD directory - multi-tenant), select web for the redirect url, fill in `http://localhost:53682/`, and finally click Register



    *** **Please see if there are errors/problems**: [Common errors and solutions/update log](https://github.com/wangziyingwen/Autoapi-test) ***

* The first step is to register an application at https://portal.azure.com/#home. There are too many online tutorials for this step, so I won’t write it in detail. I’ll give you a rough outline of the process.
   First log in to the website with the e5 administrator account, then find Azure Active Directory on the homepage and click on it. Then find the directory on the left and click Application Registration. Then click New Registration at the top and a new application interface will pop up. Fill in the application name as you like, and then Select an account in any organization directory (any Azure AD directory - multi-tenant), select web for the redirect url, fill in `http://localhost:53682/`, and finally click Register

* In the second step, after registering the application, you will jump to the application overview interface. You will see an application (client) ID. Copy this ID and record it. You will use it later. Then click on the API permissions in the left directory, and then click Click `Add Permissions`, `Microsoft Graph`, `Delegated Permissions`, then search for the following 12 permissions and check them:

   ```
   Files.Read.All Files.ReadWrite.All Sites.Read.All Sites.ReadWrite.All
   User.Read.All User.ReadWrite.All Directory.Read.Al Directory.ReadWrite.All
   Mail.Read Mail.ReadWrite MailboxSettings.Read MailboxSettings.ReadWrite
   ```

   After checking everything, click Add Permissions at the bottom, and then return to the API permissions interface. At this time, you must click `Grant administrator consent on behalf of xxx` again. If you don't click this, the Outlook API will not be able to be called.

* The third step, click on the certificate and password on the left, click + New Client Password, fill in the description as you like, select as many years as you like, and then click Add. After adding, there will be a value under the Client Password, copy the value below The string of codes, this is the application secret key, which will be used later. At this step, the application registration is over.

![Enter picture description](.github/bbb%E5%9B%BE%E7%89%87.png)

* The fourth step is to download rclone in Windows to obtain the token. [Click here to download rclone](https://rclone.org/downloads/). Download it to any directory on your computer. After downloading, do not double-click rclone.exe to install! , but in the same directory as rclone.exe, `hold down shift and right-click the mouse`, select `Open cmd window here` or `Open power shell window here`, after the window pops up, the CMD window will execute:

   ```
   rclone authorize "onedrive" "Previously saved application id" "Previously saved application key"
   ```

   Please replace the double quotes with the application id and secret key we saved before, example:

   ```
   rclone authorize "onedrive" "729xx16f-8x70-4xb8-8fd6-1xxx9b582b1f" "?@P@4u/fxxcxxx28:B-3i_QxxFxc6_ZO"
   ```

   If it is a power shell window, please execute:

   ```
   .\rclone authorize "onedrive" "729xx16f-8x70-4xb8-8fd6-1xxx9b582b1f" "?@P@4u/fxxcxxx28:B-3i_QxxFxc6_ZO"
   ```

   After execution, the computer browser will pop up an interface, log in to your e5 account, and then see the browser display `Success`!, indicating that the token has been obtained successfully. Then when we return to the cmd window or power shell window, you will see a large section of code beginning with `Paste the following into your remote machine --->` and ending with `<---End paste`. Find `"refresh_token" :"`Copy the following code until`","expiry"`. To put it bluntly, copy refresh_token without double quotes. The similar format is as follows: `OAQABAAAAAABeAFzDwllzTYxxxx_qYbH8UALCVjtv_6YeHHOwXExxxxxywOKSg2Hd_GSjW1vcLzqLhDC51Sl4T2ZYfK1p64_ps3qidrodIZL kz-4f-21IfUUgQdEi-g-jIw-La9FjREuUuQnSSKgOlBAKpiwVjwPGdaO_G9yB5cLvX5zi3MZ-_ZwEVHEp-ldDGYqQiZFSnpD6G-cjQIzuN0w8lxl_9laIH0dkA1uUOKtA64qbC976OHSIa idaF4oZi_ntQIsMHWnUssYbR- 2X446apxxMupLRM5oaHb8bKMTDlzk6_zUOw23y1jcb8gzyzL5IZdBVVX9UIuPrR-yuzyTd24v39OGk-I9xxhRms5vM6-vUPgxKzuIwFq_CYothdbo8ZvBuMJebl21D1UeaBerjPzxxxxxxxxxVQakxjMB HPC1ueyxR2UvRrlhHhNs8qYFBe5lzceofNWvy1QYRObT8DqCENyLa4Nb08jVTcA6Eh7oxkXtflg_xEY8ECRTWGIZ2qo4ziW70xxxxxxxvq6MCubQgOdt0qdWrc15LVV99YAl9L0KtC3ql0tMPVJBvodTN rvVqcxD-LNtnpxxx1J2tmDuc15xxxxxxTPp5MjXDhSbq8MACmRQh4dR09QqmqXps1c80pxyVkQbr8O669MQ1FMqlICTKJQ8c54_U9NWBo1rAU_zPmE841mDEFjy7dXakFkYR9IIthPNBr2nCQ DdvjTitCiIwcT-NTitAd7TseSpiWg9zBsd6Q1OOcL83anZnaJ4sHy68XupeFydmjIYWZw83m96xRaw5MMHJAoyeTkwkHH9qqaSZ0mNM_PN09-tj6nUVYWf5lajMNzd_0GPfwqxxxx9LC0deo43z NTZq20f94_-HNTscKg5dJOA8jUeddxxxxLQa-ZXZV38-lxxxYL_ZDvPu5-0FP-aDTwvxxxx0F7g97o3wTrHSZw14Ra9uxniTh4gAA`

![Enter picture description](.github/aaa%E5%9B%BE%E7%89%87.png)



The above is the preparation work

## Local server execution

6. Modify the following script, fill in the previously saved application ID and application key within the single quotes in lines 11 and 13 of the script, and save it as a 1.py file.

```
import requests as req
import json,sys,time,random
#Register the azure application first and ensure that the application has the following permissions:
#files: Files.Read.All, Files.ReadWrite.All, Sites.Read.All, Sites.ReadWrite.All
#user: User.Read.All, User.ReadWrite.All, Directory.Read.All, Directory.ReadWrite.All
#mail: Mail.Read, Mail.ReadWrite, MailboxSettings.Read, MailboxSettings.ReadWrite
#After registration, be sure to click on behalf of xxx to grant administrator consent, otherwise the outlook api cannot be called.

################################################ #################
#Fill in the application id within the single quotes below #
id=r''
#Fill in the application secret key within the single quotes below #
secret=r''
################################################ #################

path=sys.path[0]+r'/1.txt'
num1 = 0

def gettoken(refresh_token):
     headers={'Content-Type':'application/x-www-form-urlencoded'
             }
     data={'grant_type': 'refresh_token',
           'refresh_token': refresh)https://51.ruyo.net/15646.html

# AutoApiSecret-encrypted version

AutoApi series: AutoApi, AutoApiSecret, AutoApiSR, AutoApiS

### project instruction ###

* Use github action to realize **automatic calling of api** at regular intervals to keep E5 development active.
* **Free, no additional equipment/server required**, just forget it after deployment.
* Encrypted version, hides application ID + secret, protects account security.

### Special Instructions/Thanks ###

*Original tutorial blogger - Shady (Kuan ID-Paran): https://blog.432100.xyz/index.php/archives/50/

* Ordinary version address: https://github.com/wangziyingwen/AutoApi

* Encrypted version address (recommended): https://github.com/wangziyingwen/AutoApiSecret

* Imitate human application development version (including upgrade steps): https://github.com/wangziyingwen/AutoApiSR

* Super version address: https://github.com/wangziyingwen/AutoApiS

* **Common errors and solutions/update log**: https://github.com/wangziyingwen/Autoapi-test

* Get the refresh_token gadget from the web page (not recommended): https://github.com/wangziyingwen/GetAutoApiToken

* Video tutorial: (I operate very slowly, so I can double speed/fast forward by myself)

   * Online/download address: https://kino-onemanager.herokuapp.com/Video/AutoApi%E6%95%99%E7%A8%8B.mp4?preview

   * Station B: https://www.bilibili.com/video/av95688306/

     ​

    **The above recommendations/disrecommendations are just personal opinions, please choose the version yourself, and you can use it at the same time**.

-------------------------------------------------- ----------

### Steps ###



The first step is to register an application at https://portal.azure.com/#home. There are too many online tutorials for this step, so I won’t write it in detail. I will outline the process.
First log in to the website with the e5 administrator account, then find Azure Active Directory on the homepage and click on it. Then find the directory on the left and click Application Registration. Then click New Registration at the top and a new application interface will pop up. Fill in the application name as you like, and then Select an account in any organization directory (any Azure AD directory - multi-tenant), select web for the redirect url, fill in `http://localhost:53682/`, and finally click Register



    *** **Please see if there are errors/problems**: [Common errors and solutions/update log](https://github.com/wangziyingwen/Autoapi-test) ***

* The first step is to register an application at https://portal.azure.com/#home. There are too many online tutorials for this step, so I won’t write it in detail. I’ll give you a rough outline of the process.
   First log in to the website with the e5 administrator account, then find Azure Active Directory on the homepage and click on it. Then find the directory on the left and click Application Registration. Then click New Registration at the top and a new application interface will pop up. Fill in the application name as you like, and then Select an account in any organization directory (any Azure AD directory - multi-tenant), select web for the redirect url, fill in `http://localhost:53682/`, and finally click Register

* In the second step, after registering the application, you will jump to the application overview interface. You will see an application (client) ID. Copy this ID and record it. You will use it later. Then click on the API permissions in the left directory, and then click Click `Add Permissions`, `Microsoft Graph`, `Delegated Permissions`, then search for the following 12 permissions and check them:

   ```
   Files.Read.All Files.ReadWrite.All Sites.Read.All Sites.ReadWrite.All
   User.Read.All User.ReadWrite.All Directory.Read.Al Directory.ReadWrite.All
   Mail.Read Mail.ReadWrite MailboxSettings.Read MailboxSettings.ReadWrite
   ```

   After checking everything, click Add Permissions at the bottom, and then return to the API permissions interface. At this time, you must click `Grant administrator consent on behalf of xxx` again. If you don't click this, the Outlook API will not be able to be called.

* The third step, click on the certificate and password on the left, click + New Client Password, fill in the description as you like, select as many years as you like, and then click Add. After adding, there will be a value under the Client Password, copy the value below The string of codes, this is the application secret key, which will be used later. At this step, the application registration is over.

![Enter picture description](.github/bbb%E5%9B%BE%E7%89%87.png)

* The fourth step is to download rclone in Windows to obtain the token. [Click here to download rclone](https://rclone.org/downloads/). Download it to any directory on your computer. After downloading, do not double-click rclone.exe to install! , but in the same directory as rclone.exe, `hold down shift and right-click the mouse`, select `Open cmd window here` or `Open power shell window here`, after the window pops up, the CMD window will execute:

   ```
   rclone authorize "onedrive" "Previously saved application id" "Previously saved application key"
   ```

   Please replace the double quotes with the application id and secret key we saved before, example:

   ```
   rclone authorize "onedrive" "729xx16f-8x70-4xb8-8fd6-1xxx9b582b1f" "?@P@4u/fxxcxxx28:B-3i_QxxFxc6_ZO"
   ```

   If it is a power shell window, please execute:

   ```
   .\rclone authorize "onedrive" "729xx16f-8x70-4xb8-8fd6-1xxx9b582b1f" "?@P@4u/fxxcxxx28:B-3i_QxxFxc6_ZO"
   ```

   After execution, the computer browser will pop up an interface, log in to your e5 account, and then see the browser display `Success`!, indicating that the token has been obtained successfully. Then when we return to the cmd window or power shell window, you will see a large section of code beginning with `Paste the following into your remote machine --->` and ending with `<---End paste`. Find `"refresh_token" :"`Copy the following code until`","expiry"`. To put it bluntly, copy refresh_token without double quotes. The similar format is as follows: `OAQABAAAAAABeAFzDwllzTYxxxx_qYbH8UALCVjtv_6YeHHOwXExxxxxywOKSg2Hd_GSjW1vcLzqLhDC51Sl4T2ZYfK1p64_ps3qidrodIZL kz-4f-21IfUUgQdEi-g-jIw-La9FjREuUuQnSSKgOlBAKpiwVjwPGdaO_G9yB5cLvX5zi3MZ-_ZwEVHEp-ldDGYqQiZFSnpD6G-cjQIzuN0w8lxl_9laIH0dkA1uUOKtA64qbC976OHSIa idaF4oZi_ntQIsMHWnUssYbR- 2X446apxxMupLRM5oaHb8bKMTDlzk6_zUOw23y1jcb8gzyzL5IZdBVVX9UIuPrR-yuzyTd24v39OGk-I9xxhRms5vM6-vUPgxKzuIwFq_CYothdbo8ZvBuMJebl21D1UeaBerjPzxxxxxxxxxVQakxjMB HPC1ueyxR2UvRrlhHhNs8qYFBe5lzceofNWvy1QYRObT8DqCENyLa4Nb08jVTcA6Eh7oxkXtflg_xEY8ECRTWGIZ2qo4ziW70xxxxxxxvq6MCubQgOdt0qdWrc15LVV99YAl9L0KtC3ql0tMPVJBvodTN rvVqcxD-LNtnpxxx1J2tmDuc15xxxxxxTPp5MjXDhSbq8MACmRQh4dR09QqmqXps1c80pxyVkQbr8O669MQ1FMqlICTKJQ8c54_U9NWBo1rAU_zPmE841mDEFjy7dXakFkYR9IIthPNBr2nCQ DdvjTitCiIwcT-NTitAd7TseSpiWg9zBsd6Q1OOcL83anZnaJ4sHy68XupeFydmjIYWZw83m96xRaw5MMHJAoyeTkwkHH9qqaSZ0mNM_PN09-tj6nUVYWf5lajMNzd_0GPfwqxxxx9LC0deo43z NTZq20f94_-HNTscKg5dJOA8jUeddxxxxLQa-ZXZV38-lxxxYL_ZDvPu5-0FP-aDTwvxxxx0F7g97o3wTrHSZw14Ra9uxniTh4gAA`

![Enter picture description](.github/aaa%E5%9B%BE%E7%89%87.png)



The above is the preparation work

## Local server execution

6. Modify the following script, fill in the previously saved application ID and application key within the single quotes in lines 11 and 13 of the script, and save it as a 1.py file.

```
import requests as req
import json,sys,time,random
#Register the azure application first and ensure that the application has the following permissions:
#files: Files.Read.All, Files.ReadWrite.All, Sites.Read.All, Sites.ReadWrite.All
#user: User.Read.All, User.ReadWrite.All, Directory.Read.All, Directory.ReadWrite.All
#mail: Mail.Read, Mail.ReadWrite, MailboxSettings.Read, MailboxSettings.ReadWrite
#After registration, be sure to click on behalf of xxx to grant administrator consent, otherwise the outlook api cannot be called.

################################################ #################
#Fill in the application id within the single quotes below #
id=r''
#Fill in the application secret key within the single quotes below #
secret=r''
################################################ #################

path=sys.path[0]+r'/1.txt'
num1 = 0

def gettoken(refresh_token):
     headers={'Content-Type':'application/x-www-form-urlencoded'
             }
     data={'grant_type': 'refresh_token',
           'refresh_token': refresh
