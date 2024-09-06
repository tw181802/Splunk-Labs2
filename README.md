<img src ="https://github.com/user-attachments/assets/ebef05b3-f58d-463a-8d9a-4679fd357359" width="100">

# Splunk - Scheduling Alerts & Reports

## Login Screen

Enter your credentials

<img width="901" alt="loginscreen" src="https://github.com/user-attachments/assets/fb08cb6a-6507-4550-8d10-d23c8d13825a">





## Investigation

I have 2 indexes: `web` & `security` and 2 source types: `access_combined` and `linux_secure`.

Let's investigate one of these: type in `sourcetype=linux_secure`
<img width="950" alt="s1" src="https://github.com/user-attachments/assets/bce2c4cb-deec-4538-b794-dd929aa09c01">

Right Click Event Viewer and Examine the details

<img width="708" alt="investigate" src="https://github.com/user-attachments/assets/4504073e-d780-4582-9bc3-72052103bd75">

- **Source**: `secure.log`
- **App**: `ssh`
- **Process ID**: `5303`
- **User**: `daemon`
- **Host**: `www2` (this is a web app)

### Search Query

We can:

- Find failed root logins (e.g., `fail* root`) from the web server using:
  ```plaintext
  sourcetype=linux_secure
  
<img width="948" alt="s2" src="https://github.com/user-attachments/assets/da06ee40-2417-48e3-9115-0f0b360ec4cb">

Save it as a Report


<img width="290" alt="s3" src="https://github.com/user-attachments/assets/42843d4b-7f5f-4803-b4a2-fe3bca98fd36">

I titled mines `analyst_report_FailedRootLoginsLast24Hours`

<img width="956" alt="s4" src="https://github.com/user-attachments/assets/63abde61-76ed-4748-905d-f32797681160">

Now you can see it in the reports section and then open it in search

<img width="932" alt="s5" src="https://github.com/user-attachments/assets/8784c773-6e33-4ec8-b07c-34114256f111">


I created another report named TReport with the same search query. I am now going to click `Edit` > `Edit Schedule`

<img width="579" alt="s6" src="https://github.com/user-attachments/assets/449323a2-af8b-4719-92ec-68eb232e0648">


I have the alert scheduled to run everyday @ 6 and send email to the admin with the “Trigger Action” function

<img width="611" alt="s77" src="https://github.com/user-attachments/assets/2b29db31-9559-4ccf-8e61-35795ccd2920">

<img width="596" alt="s7" src="https://github.com/user-attachments/assets/26585fff-eb06-4ade-b347-8d214dfeaaa6">

New query

`index=security sourcetype=linux_secure failed password NOT invalid`

<img width="950" alt="s8" src="https://github.com/user-attachments/assets/e67bd1ac-bdab-4f1f-b508-0e8005ace951">


Select `Save As Alert`


<img width="632" alt="s9" src="https://github.com/user-attachments/assets/2ca4d5c8-7835-4e85-8568-5476790ca926">

<img width="600" alt="s10" src="https://github.com/user-attachments/assets/4dbefead-1333-49fc-9114-e1662f50141c">


This is how it looks when you view the alert


<img width="953" alt="s12" src="https://github.com/user-attachments/assets/f6191bd5-8ab4-45ac-98b8-3d528b0f2061">


This is how you go and find activity for the alerts

<img width="957" alt="s13" src="https://github.com/user-attachments/assets/2984d7b0-7f82-4465-a88e-416cc80dff54">




This is how it will look
<img width="960" alt="s14" src="https://github.com/user-attachments/assets/17831874-375d-41ff-b98e-5d1b05eb9975">


Then you can disable by going back to `Search & Reporting` > `Alerts` > `Edit` > `Disable`

<img width="946" alt="disable" src="https://github.com/user-attachments/assets/8c2592a8-0604-46e8-929a-851b7341aa61">

And Keep and mind you can also save the `Alert as a Report`

Now keep in mind these are the logs that are being ingested, data would vary depending on the system’s logs (this are access and secure.log)
Access log analyses can provide the following information:
number of visitors (unique first-time requests) to a specific homepage;
origin of the visitors, including their associated servers' domain name -- for example, visitors from .edu, .com and .gov sites and from other online services;
how many requests for each page on the site, presented with the pages with most requests listed first; and
use patterns related to the time of day, day of the week and season.


<img width="953" alt="logs" src="https://github.com/user-attachments/assets/ad64f4f9-4d43-428e-9464-8ceb28339f0c">


# Splunk - Statistical Processing

## Login Screen

Enter your credentials

<img width="901" alt="loginscreen" src="https://github.com/user-attachments/assets/fb08cb6a-6507-4550-8d10-d23c8d13825a">

We have different systems we can check such as web app, firewalls, game logs, badge reader, Active Directory

Scenario: The Network team wants to add a dashboard panel that displays internet usage over the last
24 hours.


<img width="957" alt="s1" src="https://github.com/user-attachments/assets/7af89960-f6d2-4216-bc9a-684ac7f6ebff">



Changed Visualization to Line Chart

<img width="950" alt="s2" src="https://github.com/user-attachments/assets/22f50531-49df-4fdf-97b2-dfc2ccee26d7">




Saved report as `L1S1`


<img width="908" alt="s3" src="https://github.com/user-attachments/assets/d13e23dd-3490-4022-abb7-265100371518">


Scenario: Security wants to add a dashboard panel that displays the top 10 IPs associated with
"Accepted" and "Failed" events on the web server.

<img width="959" alt="s3-" src="https://github.com/user-attachments/assets/03cb5ae9-cb0e-47b2-9a15-698f40ecc451">

<img width="948" alt="s4" src="https://github.com/user-attachments/assets/a723e994-fb45-4d21-bb4b-64f65b925c52">

Change Visualization to Column Chart

<img width="954" alt="s5" src="https://github.com/user-attachments/assets/366619e0-4b5a-40b6-865d-1e400a829795">

Now using the top command to id which domain website visitor use ; `limit` command shows top 2

<img width="958" alt="s6" src="https://github.com/user-attachments/assets/416bcf3f-d8f8-41ff-9b20-948600cb4f3c">

To eliminate the percentage we need to add `showperc=f referer_domain`

<img width="955" alt="s7" src="https://github.com/user-attachments/assets/bfd925f7-c4e7-45d8-9f62-49a702e06bbf">


Now let’s look at the badge reader logs

<img width="953" alt="s8" src="https://github.com/user-attachments/assets/1832d211-00f1-46ae-a790-d08676d7f35c">


Used stats to filter out location values

<img width="958" alt="s9" src="https://github.com/user-attachments/assets/6c8ea4ef-f298-4b17-9622-2d8517777df5">


Filter to show usernames and change the count field to Badged in Employees

<img width="960" alt="s10" src="https://github.com/user-attachments/assets/e213adab-768b-4243-9b1e-ba34e19527e0">

Changed Visualization to bar chart

<img width="951" alt="s11" src="https://github.com/user-attachments/assets/041c2239-91e5-41de-a45d-bd3b44cfb3c2">




Security wants to know what content employees are viewing on the network

<img width="954" alt="s12" src="https://github.com/user-attachments/assets/245ab9fd-097d-4940-8b95-f2ea6b39d2c7">

Find the 3 most uncommon media types

<img width="959" alt="s13" src="https://github.com/user-attachments/assets/1ec6303b-9087-46d0-9273-d5a1d3fcac68">

Sales want to know 5 best selling products in NA over the week


<img width="958" alt="s14" src="https://github.com/user-attachments/assets/761ba237-8d57-46be-bf9c-35763e7be47e">

Filter by products

<img width="951" alt="s15" src="https://github.com/user-attachments/assets/844d8265-634a-4d47-8bb6-2e220837c897">

How to remove the “OTHER” category and just show the top 5

<img width="957" alt="s16" src="https://github.com/user-attachments/assets/dc324a48-ad91-4ed1-a727-8d62420147ae">

Now we will manipulate the data with eval command 
Scenario : Sales want to know the total events, average price and total price for each action performed by visitors to the online store during the prev week.
We will calculate the total events by action
Calc the avg price and sum of price by each action
Rename the count,avg,sum field as total events, avg price, and total amt
Round total amt and avg price value to two decimal places
Sort total amt by descending order
`index=web sourcetype=access_combined | stats count, avg(price) , sum(price) by action | rename count as "Total Events", avg(price) as "Average Price", sum(price) as "Total Amount" | eval "Total Amount"=round('Total Amount',2), "Average Price"=round('Average Price', 2) | sort -"Total Amount"`


<img width="957" alt="s16" src="https://github.com/user-attachments/assets/ada1f843-2042-4df2-8a51-0f3826a94d1f">


Scenario: Networking wants to know daily volume (in MB) handle by the Buttercup Games online 




Will be charted with timechart and eval to convert bytes to MB
Timechart and sum will calc the total bytes consumed each day 

<img width="959" alt="s17" src="https://github.com/user-attachments/assets/328b238f-7bdc-49fa-b079-e17344f750d1">

Now I will use eval command to create new field called “megabytes”
Convert bytes to megabytes with `bytes(1024*1024)`
Round the results of this calc to 2 decimal places

<img width="960" alt="s18" src="https://github.com/user-attachments/assets/babff48d-9f35-4bdc-871b-06a22838a1fe">


I rewrote the search so that the eval command uses the round and pow command convert bytes to megabytes
`index=web sourcetype=access_combined | timechart sum(bytes) as bytes | eval megabytes =round(bytes/pow(1024,2),2)`

<img width="960" alt="s18" src="https://github.com/user-attachments/assets/488ab137-3959-468f-ad61-67588f4c0a65">





Scenario: Networking wants to know the total number of GET and POST req and the ratio of GET to POST req for each web server over the last 4 hrs. Then edit teh search round the values of ratio



Use `round(GET/POST,2)`

<img width="959" alt="s19" src="https://github.com/user-attachments/assets/9894efd0-de5b-41ec-824d-e47d1f69fb53">

<img width="954" alt="s20" src="https://github.com/user-attachments/assets/83d541ed-44f4-41b6-9a72-a8dc25538837">

Scenario: The Sim Cubicle Beta team needs help randomly generating phone numbers for characters in the game. Use the random function to generate fake number for players


The `dedup` commands removes all duplicate values for CharacterName. The format should be using the format 555-XXXX where the last 4 digits are btw 0-9.  Change the search from over All Time.

`index=games sourcetype=SimCubeBeta | dedup CharacterName | eval phoneNumber = "555"."-".(random() % 10).(random() % 10).(random() % 10).(random() % 10 ) | table CharacterName phoneNumber`
NOTE: phoneNumber can literally be named anything phNumber , pHonY, etc.

<img width="958" alt="s21" src="https://github.com/user-attachments/assets/dbb9575e-aad2-4242-87d5-3337ccd37e1f">


Scenario:Sales want to know which one-hour intervals over the last 24 hrs have Buttercup Games online sales been twice as profitable as sales in retail stores

We will use `timechart` and `sort` commands to create a report that shows the hours where web sales were twice as much retails sales in descending order




<img width="958" alt="s22" src="https://github.com/user-attachments/assets/6fbfd82b-5bff-4c94-92df-f81e56d48aa4">


We can use `where` command to only keep events where the web sales values are more than twice as much as retail sale values

<img width="958" alt="s24" src="https://github.com/user-attachments/assets/b1707b3e-17a6-42d9-8e02-40deb7109355">


Sort where results are descending order based on the web sales values

<img width="958" alt="s25" src="https://github.com/user-attachments/assets/082aa9e4-061a-4011-9807-7a5bbe6a5ab9">


Scenario: Sales wants to know which products had online sales of more than $15000 during the last 30 days

Can be fulfilled using stats, eval, sort, and rename commands



Use where command to show products with over $15000

`index=web sourcetype="access_combined" action=purchase status=200 | stats sum(price) as sales by product_name | where sales > 15000`

<img width="957" alt="s27" src="https://github.com/user-attachments/assets/5213fc9f-ce7c-4fc0-b993-cb32750e9fed">



To round to whole number you’ll use

`index=web sourcetype="access_combined" action=purchase status=200 | stats sum(price) as sales by product_name | where sales > 15000 | eval sales=round(sales,0)`

<img width="959" alt="s28" src="https://github.com/user-attachments/assets/64f404b9-d859-4a55-8997-f27ae947b594">




Sort values descending order and rename product name as “Best Sellers” and sales as “Total Revenue”
`index=web sourcetype="access_combined" action=purchase status=200 | stats sum(price) as sales by product_name | where sales > 15000 | eval sales=round(sales,0) | sort -sales | rename product_name as "Best Sellers", sales as "Total Revenue"`


<img width="960" alt="s29" src="https://github.com/user-attachments/assets/138edea3-7ae4-46d1-bc8c-9192ac68909c">


Now you can save the report


Scenario: ITops want to see most common status codes for each of the web server using the top command (find top 2 status code values during last 24 hrs)




To split server host values
`index=web sourcetype="access_combined" | top limit=2 status by host`

<img width="956" alt="s30" src="https://github.com/user-attachments/assets/0d26a486-ab3f-48e1-be2f-09b62b25516b">



Can remove the count column with `| fields - count`

<img width="957" alt="s31" src="https://github.com/user-attachments/assets/159858e2-f6b8-4192-bb9d-c716ecc5b2a3">


You can also use `showcount=f` (which is boolean meaning it can be equal to true or false value)
Ex.



<img width="957" alt="s32" src="https://github.com/user-attachments/assets/46bc4ff2-82db-4d58-a2c8-ec2578e5a270">


