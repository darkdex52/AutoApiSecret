https://51.ruyo.net/15646.html

# AutoApiSecret-encrypted version

AutoApi series: AutoApi, AutoApiSecret, AutoApiSR, AutoApiS

### project instruction###

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
First log in to the website with the e5 administrator account, then find Azure Active Directory on the homepage and click on it, then find it on the left directory and click Application Registration. Then click New Registration at the top and a new application interface will pop up. Fill in the application name as you like, and then Select an account in any organization directory (any Azure AD directory - multi-tenant), select web for the redirect url, fill in `http://localhost:53682/`, and finally click Register



*** **Please see if there are errors/problems**: [Common errors and solutions/update log](https://github.com/wangziyingwen/Autoapi-test) ***

* The first step is to register an application at https://portal.azure.com/#home. There are too many online tutorials for this step, so I won’t write it in detail. I’ll give you a rough outline of the process.
First log in to the website with the e5 administrator account, then find Azure Active Directory on the homepage and click on it, then find it on the left directory and click Application Registration. Then click New Registration at the top and a new application interface will pop up. Fill in the application name as you like, and then Select an account in any organization directory (any Azure AD directory - multi-tenant), select web for the redirect url, fill in `http://localhost:53682/`, and finally click Register

* In the second step, after registering the application, you will jump to the application overview interface. You will see an application (client) ID. Copy this ID and record it. You will use it later. Then click on the API permissions in the left directory, and then click Click `Add Permissions`, `Microsoft Graph`, `Delegated Permissions`, then search for the following 12 permissions and check them:

```
Files.Read.All Files.ReadWrite.All Sites.Read.All Sites.ReadWrite.All
User.Read.All User.ReadWrite.All Directory.Read.Al Directory.ReadWrite.All
Mail.Read Mail.ReadWrite MailboxSettings.Read MailboxSettings.ReadWrite
```

After checking everything, click Add Permissions at the bottom, and then return to the API permissions interface. At this time, you must click `Grant administrator consent on behalf of xxx` again. If you don't click this, the Outlook API will not be able to be called.

* The third step, click on the certificate and password on the left, click + New Client Password, fill in the description as you like, select as many years as you like, and then click Add. After adding, there will be a value under the Client Password, copy the value below The string of codes, this is the application secret key, which will be used later. At this step, the application registration is over.

![Enter picture description](.github/bbb%E5%9B%BE%E7%89%87.png)

* The fourth step is to download rclone in Windows to obtain the token. [Click here to download rclone](https://rclone.org/downloads/). Download it to any directory on your computer. After downloading, `Do not double-click rclone.exe to install!` , but in the same directory as rclone.exe, `hold down shift and right-click the mouse`, select `Open cmd window here` or `Open power shell window here`, after the window pops up, the CMD window will execute:

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
'refresh_token': refresh_token,
'client_id':id,
'client_secret': secret,
'redirect_uri':'http://localhost:53682/'
}
html = req.post('https://login.microsoftonline.com/common/oauth2/v2.0/token',data=data,headers=headers)
jsontxt = json.loads(html.text)
refresh_token = jsontxt['refresh_token']
access_token = jsontxt['access_token']
with open(path, 'w+') as f:
f.write(refresh_token)
return access_token
def main():
fo = open(path, "r+")
refresh_token = fo.read()
fo.close()
globalnum1
access_token=gettoken(refresh_token)
headers={
'Authorization':access_token,
'Content-Type':'application/json'
}
try:
if req.get(r'https://graph.microsoft.com/v1.0/me/drive/root',headers=headers).status_code == 200:
num1+=1
print("1 call successful"+str(num1)+'times')
if req.get(r'https://graph.microsoft.com/v1.0/me/drive',headers=headers).status_code == 200:
num1+=1
print("2 call successful"+str(num1)+'times')
if req.get(r'https://graph.microsoft.com/v1.0/users ',headers=headers).status_code == 200:
num1+=1
print('3 call successful'+str(num1)+'times')
if req.get(r'https://graph.microsoft.com/v1.0/me/messages',headers=headers).status_code == 200:
num1+=1
print('4 call successful'+str(num1)+'times')
if req.get(r'https://graph.microsoft.com/v1.0/me/mailFolders/inbox/messageRules',headers=headers).status_code == 200:
num1+=1
print('5 call successful'+str(num1)+'times')
if req.get(r'https://graph.microsoft.com/v1.0/me/mailFolders/inbox/messageRules',headers=headers).status_code == 200:
num1+=1
print('6 call successful'+str(num1)+'times')
if req.get(r'https://graph.microsoft.com/v1.0/me/drive/root/children',headers=headers).status_code == 200:
num1+=1
print('7 call successful'+str(num1)+'times')
if req.get(r'https://api.powerbi.com/v1.0/myorg/apps',headers=headers).status_code == 200:
num1+=1
print('8 call successful'+str(num1)+'times')
if req.get(r'https://graph.microsoft.com/v1.0/me/mailFolders',headers=headers).status_code == 200:
num1+=1
print('9 call successful'+str(num1)+'times')
if req.get(r'https://graph.microsoft.com/v1.0/me/outlook/masterCategories',headers=headers).status_code == 200:
num1+=1
print('10 calls successful'+str(num1)+'times')
except:
print("pass")
pass
while True:
main()
for i in range(random.randint(150,300),0,-1):
print("\r"+str(i)+'The next round of calls will start in seconds', end='')
time.sleep(1)
```

After saving the script, create a file named 1.txt in the same directory as the script. Copy the large token starting with OAQ obtained in step 4 into 1.txt, save and exit.

Save both 1.py and 1.txt and then upload them to the server. Make sure that the two files 1.py and 1.txt are in the same directory.

7. The server needs to install python3, and install pip3 and requests. If it is a Linux server, you need to use the screen window to run it.

After installation, you can run 1.py to flash the script.



The above is a tutorial for flashing office e5 through scripts. Both windows and linux servers can be used. However, many people may not have their own servers. It is not cost-effective to purchase the script separately. Therefore, some experts use github action to automatically call the api at regular intervals. , keeping E5 development active. This will be updated later.





## github action automatically executed



* In the first step, use the previous application id, secret, and refresh_token to facilitate the next operation.

* The second step is to log in/create a github account, return to the project page, click on the upper right corner to fork the code of this project to your own account, and then an identical project will appear under your account, and the next operations are all in your under this project. (If you can’t see the picture/please browse the internet scientifically)

* Get the application id, secret, refresh_token (copy and save it yourself, be careful to distinguish the id secret, don't get confused)

Then edit 1.txt in your project online and paste the entire refresh_token into it (my data is inside, delete or overwrite it first). (Never change 1.py)

> The location of refresh_token is as shown below. Copy the content in the double quotes immediately following refresh_token (framed by a red vertical line). Do not copy the double quotes. After copying into 1.txt, be careful not to leave any spaces or blank lines at the end.

 

* The third step, click Setting > Secrets > Add a new secret in the upper column, and create two new secrets as shown in the figure: CONFIG_ID, CONFIG_KEY.

The contents are as follows: (Change your application ID to your application ID, change your application secret to your secret, leave the single quotes alone)

CONFIG_ID

```shell
id=r'your application id'
```

CONFIG_KEY

```shell
secret=r'your application secret'
```


The final format should look like this:

![Enter picture description](.github/workflows/%E5%9B%BE%E7%89%87.png)



* The fourth step, enter your personal settings page (the avatar Settings in the upper right corner, not the Settings in the warehouse), select Developer settings > Personal access tokens > Generate new token,

Set the name to GITHUB_TOKEN, then check options such as repo, admin:repo_hook, workflow, etc., and finally click Generate token.
 
 
 
* The fifth step, click on the star/star in the upper right corner to call it immediately, and then click on the Action above to see each operation log and see the operation status.

(You must click on Test Api to see if the api is called in place and if there are any errors. The Auto Api checkmark outside can only indicate that the operation is normal. We also need to confirm that the 10 api calls are successful, just like in the picture .If there are several APIs missing, either the API permissions were not given properly when registering the application; or the OneDrive is not activated by logging in, please log in and activate it)

* Step 6, if there are no mistakes, it’s done! ! Check again to see if you want to modify the following timing times. If you don’t plan to change it, just ignore it.

**Then come back the next day to confirm whether it runs automatically (whether there are a few more in the ation)**, if so, don't worry about it, it's over.

I set it to run automatically every 3 hours, with 3 rounds of calls each time (you can also call it immediately by clicking on the star/star in the upper right corner). You can modify it at your own discretion (I don’t know how many times and how long it takes to stay active):

* Scheduled automatic start modification place: (In the .github/workflow/AutoApiSecret.yml file, customize the Baidu cron scheduled task format, at least once every 5 minutes)

* The place to modify each round: (at the end of 1.py)


-------------------------------------------------- ----------

### Off topic###

>Api call
> You can take a look at Graph Browser yourself and learn to modify what APIs you want to call (the most important thing is to call Outlook and OneDrive)
> https://developer.microsoft.com/zh-CN/graph/graph-explorer/preview

### Introduction to GithubAction###

Provided virtual environments:

· 2-core CPU
· 7 GB RAM memory
· 14 GB SSD hard drive space

Usage restrictions:

* Each warehouse can only support 20 parallel workflows at the same time.
* GitHub API can be called 1000 times per hour.
* Each job can be executed for up to 6 hours.
* Users of the free version support a maximum of 20 jobs for concurrent execution, while macOS only supports a maximum of 5.
* The cumulative usage time of private warehouses is 2000 minutes per month, and $0.008/minute after exceeding. There is no limit for public warehouses.

(The public warehouse we use here, logically, you can set up an infinite loop call, and then start it every 6 hours, ensuring 24-hour call)

### at last###

The tutorial is very straightforward, you should know how to do it!



**Common mistakes and Q&A**

Why is the error reported?
Traceback (most recent call last):
File "1.py", line 83, in
main()
File "1.py", line 40, in main
access_token=gettoken(refresh_token)
File "1.py", line 33, in gettoken
refresh_token = jsontxt['refresh_token']
KeyError: 'refresh_token'

Answer: This is because the refresh_token you obtained using rclone is incorrect. Most likely, you copied it incorrectly. It must be a string starting with OAQ and without double quotes!

Do I need to download rclone.exe to obtain the token when using Ubuntu or Debian?
Answer: Yes, the function of rclone is to obtain the token. Microsoft's API requires you to bring the token to access it successfully, so no matter which platform, you must use rclone.exe to obtain the token.

Does it require a server?
Answer: Not necessarily. As long as the platform can use python3, it can be used. You can install python3 on Baidu windows, or download termux on your Android phone to install python3. You can find out how to do it by yourself.

How long will the script hang?
Answer: Microsoft does not have a clear indicator, so the longer the default is, the better. Therefore, it is recommended to hang on the server 24 hours a day.

What does screen do?
Answer: screen is used on the server. Generally, if our server executes the script and disconnects the ssh script, the script will be disconnected, so we use screen -S api to open a new screen named api. Even if the ssh is disconnected, the script is still there. Run in the background. The next time you connect to SSH, execute screen -r api to check the execution of the script. If the script is hung in Windows, you don't need screen.
