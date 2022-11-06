# Postmortem for a failed server

![Failed Server](https://miro.medium.com/max/1400/1*P-Zu0RX33TUT0S6yyFNPYA.jpeg)
* Summary


    Duration of outage: Nov. 5th, 2022 at about 15:14 GMT to 16:30 GMT, over 4000 users/visitors couldn’t access the company’s wordpress site and the subdomins, nor could they contact the support team via the support forms on the site, this totally reduced the functionality of the website. 
    Root cause: the NGINX configuration was poorly modified by one of the engineers and restarted the server without checking for syntax.

![Reboot Server](https://media-exp1.licdn.com/dms/image/C4E12AQGHxL6jNsOb0g/article-cover_image-shrink_600_2000/0/1612553085336?e=2147483647&v=beta&t=CwYEG94zJ_N6Nn6dHfVfy2STNRXuP4z5Jrb0bRf6UFs)



* Timeline

    - 15:20 - users started reporting the error
    - 15:30 — the team noted the frequent reports and started assessing the situation
    - 15:40 - every hardware and server was checked for a hardware failure
    - 16:15 - the error on the config file of NGINX was detected, and it was corrected
    - 16:20 - the NGINX restart
    - 16:30 - The site got back to Normal



* Root cause

    The NGINX configuration was edited by one of the engineers and restarted the server with out checking for syntax.
    ![Wrong NGINX Configuration](https://bs-uploads.toptal.io/blackfish-uploads/uploaded_file/file/194520/image-1582751182464-4b9d62e62912bd777a7c647a8309df8b.png)



* Resolution and Recovery.
![A Call to Fix Server](http://www.quickmeme.com/meme/353aoe)
    - At 15:30 PM, a ticket was opened to fix the down server and sent out to the database service provider personnel.
    - The NSX CLI is used to get detailed information about tail logs and take packet captures. It also, looks at the metrics for trouble shooting the load balancer.
    - Verification of basic services are running by checking the routing table.
    - To help with recovery, we retarted affected servers. SRE engineers, manually restarted unicorn processes on the web application servers to further correct the reboot process.
    - The process was slow to prevent any possible cascading failures and to avoid a wide scale reboot — affecting our customers even further.
    - By 16:30 PM, traffic was restored and 100% of our customers reported back with no issues.



* Corrective and preventative measures


    In the last 3 days, we’ve made an internal review and analysis of the outage. The following measures are actions the team will follow for prevention and to improve response times in the future.


    - Monitoring mechanisms like data-dog must be used.
        The database server provider during the performance degradation could have alerted teams by noting that the down server was not routine behavior. An update to their systems to prevent further issues in the future are done accordingly.
    - The Security Team did not properly plan the reboot schedule affecting many of our customers. There was no available staff to monitor the reboot and to access the situation right away in a timely manner.


    There were no engineers present to possibly resolve the situation by manually fixing any issues that came up.
    For scheduled reboots like this, there should be a 24 hour operations rotation in order to monitor every aspect of the update.

    ![Server be Good](https://pics.me.me/yeah-tech-support-i-think-the-server-is-down-ok-43898165.png)