# Cybersecurity Pre-work: Brute force attacks

## 1. The Mission

The owner of a blog has contracted your security firm to test their website for vulnerabilities.

Your mission is to hack into their blog. You suspect that you can find a user whose password is too simple. First, you need to find a registered user, and then you're going to attempt dozens of different common passwords.

This would be a tedious process, but luckily, you have Burp, and its trusty Intruder tool that's built for this very purpose.

## 2. Setup

1. [Install Burp](https://guides.codepath.org/websecurity/Installing-Burp) - Burp is used by cybersecurity professionals everywhere to view network traffic and test for security vulnerabilities.
2. [Create a Portswigger account](https://portswigger.net/users/register) - Portswigger is the maker of Burp and has an [Academy](https://portswigger.net/web-security) to hone your cybersecurity skills.

:::info

<img alt="link" title="link" src="/images/emoji/unicode/1f517.png"}" style="vertical-align:middle" width="20" height="20" /> Important Links:

- [Username Enumeration via Different responses](https://portswigger.net/web-security/authentication/password-based/lab-username-enumeration-via-different-responses)
- [Candidate usernames](https://portswigger.net/web-security/authentication/auth-lab-usernames)
- [Candidate passwords](https://portswigger.net/web-security/authentication/auth-lab-passwords)

:::

### Step 1: Find the login url

1. Login to your [Portswigger account](https://portswigger.net/users)
<img src='https://imgur.com/NCuG3CI.png' title='Portswigger' width='' alt='Portswigger' />

2. Fire up Burp, and attempt to login to [the blog](https://portswigger.net/users?returnurl=%2facademy%2flabs%2flaunch%2fbb33e208e844c60faa4fe5876260053b536745d65312212a398ef5799fad29c8%3freferrer%3d%252fweb-security%252fauthentication%252fpassword-based%252flab-username-enumeration-via-different-responses) with a **RANDOM** username and password. The blog login looks like the image below. If you see the Portswigger login, you should login with your Portswigger account credentials first, then it will redirect you to the blog page.
<img src='https://imgur.com/BhWP2tJ.png' title='Blog Login' width='' alt='Blog Login' />
3. In Burp, go to **"Proxy"** -> **"HTTP history"**, and find the network request of the attempted login. You'll recognize it because it's a POST request to the login url of the blog.

4. Right-click the request and click "Send to Intruder"
<img src='https://i.imgur.com/oh8aeTT.png' title='Burp HTTP Requests' width='' alt='Burp HTTP Requests' />

:::info

Not seeing any requests? Check the intercept. **"Proxy"** -> **"Intercept"** and click the intercept button to say **"Intercept is off"**

:::

### Step 2: Find a registered user

Burp Intruder allows you to make the same request over and over again, except you can specify a part of the request to change. This makes it perfect for attempting to login as many different users with thousands of passwords, known as a brute force attack.

1. In Burp Intruder, go to the **"Positions"** tab. Make sure that the attack type [**"Sniper"**](https://portswigger.net/burp/documentation/desktop/tools/intruder/positions) is selected.
2. Click **"Clear"** to remove any automatically assigned payload positions. In the username parameter, highlight the value and click **"Add"** to add a payload position to this parameter. This position will be indicated by two § symbols, for example: **username=§random_username§**
<img src='https://i.imgur.com/CZyjonI.png' title='uIntruder' width='' alt='uIntruder' />

3. Do not change anything related to the password for now.
4. On the **"Payloads"** tab, select palyload set -> **"1"** and payload type -> **"Simple list".**
5. Under "Payload options", paste the list of [candidate usernames](https://portswigger.net/web-security/authentication/auth-lab-usernames) and click "Start attack". The attack will start in a new window.
<img src='https://i.imgur.com/vf7Zjej.png' title='Username Payload' width='' alt='Username Payload' />

6. When the attack is finished, on the **"Results"** tab, examine the **"Length"** column. Click on the column header to sort the results. Notice that one of the entries is different to the other ones -- usually, 3186 is the one with a successful username.
7. Examine this response. Notice that other responses contain the message Invalid username, but this response says Incorrect password. Take note of this username. **The successful username will vary for each login and will only works until the session is valid.**

If you've completed the steps above, you've identified the username of a registered user of the blog, although you don't know their password...yet.

### Step 3: Find the password

Now that you have a registered user, you want to attempt to login as that user with dozens of simple passwords.

1. Close the attack and go back to the **"Positions"** tab. Click **"Clear"** again and change the username parameter to the username you just identified. Add a payload position to the password parameter.Now you should see something like this **username=identifiedUser&password=§invalid-password§**
2. On the "Payloads" tab, clear the list of usernames and replace it with the list of [candidate passwords](https://portswigger.net/web-security/authentication/auth-lab-passwords). Then click "Start attack".
3. When the attack is finished, look at the "Status" column. Notice that each request returned a 400 status code, until eventually one returns 302. This suggests that the login attempt was successful. Take note of the password.
<img src='https://i.imgur.com/PEyiOAv.png' title='password attack' width='' alt='password attack' />

4. Back in your browser, click the "Login" link in the upper-right corner to open a fresh login page and using the username and password that you identified. You must click "My account" to solve the lab.

Congratulations, young apprentice, you've hacked your first site! The blog owner is grateful to you for reporting a vulnerable user.

:::info

**Getting an error?**

- Make sure you are only sending one request to the site. Sending multiple request will result in different sessions casuing a timeout error.
- In general the sesssion will expire ever 15 minutes. You may need to redo the challenge if you exceed the time.
- CSRF error? The CSRF token in the request is no longer valid as it was already used to succesfully login. Use a [fresh login page](https://acae1f321e738e3a805597a6006d0077.web-security-academy.net/login) to avoid an error.

:::

## 3. Submission

1. Go to the [Hall of Fame](https://portswigger.net/web-security/hall-of-fame), scroll to the bottom, and take a screenshot of your entry. The bottom of the screenshot must include your username and indicate the completion of the lab with **"1 of ###".**
<img src='https://i.imgur.com/ZvhdrY6.png' title='Hall of Fame' width='' alt='Hall of Fame' />

2. Go to GitHub and create a [new repository](https://github.com/new) to store your work for the class.
3. Add your screenshot to your repository by clicking **"upload an existing file".**
<img src='https://i.imgur.com/w1BoOR3.png' title='github' width='' alt='github' />

4. Go to the [CodePath application status dashboard](https://apply.codepath.org/dashboard/) and then press the "SUBMIT" button in the pre-work section:
  [<img src='https://i.imgur.com/GQa79TZ.png' title='Prework Submit' width='' alt='Prework Submit' />](https://apply.codepath.org/dashboard)
5. In the pre-work submission form, link to your GitHub repo.

# Still have questions about pre-work?

* If you encounter technical difficulties while submitting your work, please join our Pre-work Support Workspace **[here](https://go.codepath.org/preworkslack)**. 
  - This [workspace](https://go.codepath.org/preworkslack) is intended to support applicants with pre-work completion difficulties. 
  - Make sure to join and [create an account](https://go.codepath.org/preworkslack) with us to get assistance from our awesome team of tech experts and other students who may have encountered the same technical issues as yours!
