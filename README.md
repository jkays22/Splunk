# Splunk
# Vandalay Industries Monitoring 

# Step 1: The Need for Speed

Background: As the worldwide leader of importing and exporting, Vandalay Industries has been the target of many adversaries attempting to disrupt their online business. Recently, Vandaly has been experiencing DDOS attacks against their web servers.
Not only were web servers taken offline by a DDOS attack, but upload and download speed were also significantly impacted after the outage. Your networking team provided results of a network speed run around the time of the latest DDOS attack.

# Task: Create a report to determine the impact that the DDOS attack had on download and upload speed. Additionally, create an additional field to calculate the ratio of the upload speed to the download speed.

Uploading ‘Speed Test’ file then using the eval command to create a field called ratio that shows the ratio between the upload and download speeds. Formatting the ratio is: | eval new_field_name = 'fieldA' / 'fieldB'


![eval_ratio](https://user-images.githubusercontent.com/88590862/140990568-258bddd9-a0e5-42de-9d31-220202eded8f.PNG)


Next I will create a report using the Splunk's table command to display the following fields in a statistics report. I’ll use the following format for the table command: | table fieldA, fieldB, fieldC

_time
IP_ADDRESS
DOWNLOAD_MEGABITS
UPLOAD_MEGABITS
ratio

![ST_table](https://user-images.githubusercontent.com/88590862/140990873-996588f5-8eff-4a89-a579-096d0b5cfda8.PNG)
![event_clue](https://user-images.githubusercontent.com/88590862/140990892-4a8b563a-5279-4610-b924-ea1dfbc5de41.PNG)
![visualized_clue](https://user-images.githubusercontent.com/88590862/140990901-228ded0b-50d5-4236-bc0b-90ce454848b8.PNG)


Based on the report created and other tools in Splunk, we find the approximate date and time of the attack occurred on 02/23/2020 at 2:30pm and lasted until 02/23/2020 at 11:30pm. The systems took about 9 hours to recover.

# Step 2: Are We Vulnerable?

Background: Due to the frequency of attacks, your manager needs to be sure that sensitive customer data on their servers is not vulnerable. Since Vandalay uses Nessus vulnerability scanners, you have pulled the last 24 hours of scans to see if there are any critical vulnerabilities.

# Task: Create a report determining how many critical vulnerabilities exist on the customer data server. Then, build an alert to notify your team if a critical vulnerability reappears on this server.

I have uploaded our Nessus file and determined  how many critical vulnerabilities exist on the customer data server using the below information:

The database server IP is 10.11.36.23.
The field that identifies the level of vulnerabilities is severity.
![critical_cmd](https://user-images.githubusercontent.com/88590862/140991034-defe2973-739d-4bfc-8697-9d3c909f2bb6.PNG)

![severity_amount](https://user-images.githubusercontent.com/88590862/140991079-e752cdd4-eea6-4fe1-a963-ff41d889b24b.PNG)

I then built an alert that monitors every day to see if this server has any critical vulnerabilities. If a vulnerability exists, the alert is emailed to soc@vandalay.com

![alert1](https://user-images.githubusercontent.com/88590862/140991163-a3fb730b-273a-4280-8209-942c8f71ae06.PNG)
![alert2](https://user-images.githubusercontent.com/88590862/140991199-88835446-21ec-4c0b-ac7e-4a158ceccb34.PNG)
![finalized_alert](https://user-images.githubusercontent.com/88590862/140991233-a36e84aa-f839-46af-b0f5-65c2d9bd77df.PNG)


I’ve also created a scheduled email sending the critical vulnerability report every week for additional monitoring and information:

![scheduled_report](https://user-images.githubusercontent.com/88590862/140991290-e10dc41b-d4bd-47c4-b2b6-81f35b742172.PNG)
![scheduled_report2](https://user-images.githubusercontent.com/88590862/140991292-a58f1617-a82a-466a-af3e-6f96496378c6.PNG)



# Step 3: Drawing the (base)line

Background: A Vandaly server is also experiencing brute force attacks into their administrator account. Management would like you to set up monitoring to notify the SOC team if a brute force attack occurs again.

# Task: Analyze administrator logs that document a brute force attack. Then, create a baseline of the ordinary amount of administrator bad logins and determine a threshold to indicate if a brute force attack is occurring.

I have uploaded the admin logs and found out when the brute force attack occurred using the below information to make the event easier to identify.

Look for the name field to find failed logins.
![brute_start](https://user-images.githubusercontent.com/88590862/140991389-6abcf095-5693-4095-93bf-457aefea5d8d.PNG)


The attack started to spike at 9 am on 02/21/2020. The attack started to slow down after 1 pm the same day. The attack lasted about 4 hours. 
I have determined a baseline of normal activity and a threshold that would alert if a brute force attack is occurring to be about 15. 


I then designed an alert to check the threshold every hour and email the SOC team at SOC@vandalay.com if triggered.

![BF_alert](https://user-images.githubusercontent.com/88590862/140991455-9b2c2282-4d69-419e-9f49-af2577cb183c.PNG)
![BF_alert2](https://user-images.githubusercontent.com/88590862/140991461-2fd30389-da98-4606-b333-efc4faf19ff0.PNG)
![BF_alert_final](https://user-images.githubusercontent.com/88590862/140991472-be481f8a-d30a-4df8-9ba8-d9e2485abb34.PNG)


