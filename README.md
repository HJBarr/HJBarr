# Splunk Project

### In this splunk sceneario I use splunk to analyze a simulated attack  


# First Part Of Attack Windows Server Log 

Before 
![Screenshot (106)](https://github.com/user-attachments/assets/c6202b41-f07c-4a0f-81c2-803ea008d3dc)

After Here we can se a spike on high severity which means there was a type of attack 
![Screenshot (107)](https://github.com/user-attachments/assets/3ba54cd9-3bed-4690-a74b-8dbd84e5fbcc)

After further analysing them we found a suspices spike on faild activities and on succesful log ins which leads me to belive that access was gained thru brute force 

Faild activities 
![Screenshot (90)](https://github.com/user-attachments/assets/c317c201-0612-4159-afef-2460018861f1)
Succesful log ins 
![Screenshot (89)](https://github.com/user-attachments/assets/78120c17-9582-4a62-9f0a-e0f033419910)

2 Signatures had big increase after the attack those being accounts being locked out and attempts being made to reset a users password and 2 users also stood out 
This activitie lead me to belive that thru the brute force attack they gained access to this accounts and chnaged this users passwords for easeier access 
User account being locked out 
![Screenshot (93)](https://github.com/user-attachments/assets/0b5559e6-702d-4983-bd41-6f9f94154930)
Attempts to reset password 
![Screenshot (94)](https://github.com/user-attachments/assets/2c15e4ed-dccc-4e58-b09d-0d592c11aa63)
Users
![Screenshot (96)](https://github.com/user-attachments/assets/cdbc4eb6-6ad8-4fab-bd04-23452668dcc6)

 # Second Part Of Attack Apache Web Server (linux machine)

After analyzing the logs I encounter a surge on POST going from 106 to 1324 and a decrease in GET from 9851 to 3157 as well as an increase on Code 404 going from 213 to 679 all this data makes me belive there was a DDoS attack on the web server 

Before Method ![Screenshot (72)](https://github.com/user-attachments/assets/333faa02-b13a-4a6c-9e6f-83a6c896f5f8)

After Method ![1BWuXuz14Glv5PhR0QIJDoyKF3-8qXfiEE94Sak0jJlk](https://github.com/user-attachments/assets/96707353-8ee7-4983-ab0f-3f8d4b3ce7d9)

Before Status ![Screenshot (97)](https://github.com/user-attachments/assets/1493dcaa-c4f3-4f1f-b943-46eeb28e260b)

After Status ![Screenshot (98)](https://github.com/user-attachments/assets/192366ba-fccf-411d-9982-875783d29449)

Decrease on website visits 

Before ![Screenshot (73)](https://github.com/user-attachments/assets/efaebdc6-9958-4ae9-b97c-09dceae4f543)
 
After ![Screenshot (99)](https://github.com/user-attachments/assets/068429c6-3f7a-4336-af68-cb3388160809)

After looking at the URI I was able to pinpoint the attack to the /VSI_Account_logon.php we can see that the POST request match to it which means the DDoS attack was oerform on the logon page 
![Screenshot (126)](https://github.com/user-attachments/assets/6f4a116d-1571-4fd5-96fb-ac8daa313b62)

I was also able to use a cluster map to see where the main concentration of POST request where coming from Ukraine
![Screenshot (127)](https://github.com/user-attachments/assets/418c350e-2dcc-4698-b43e-8d50da94f399)

# Incident Summary 
## Brute Force Attack on user_J:
- Attackers successfully compromised user_J’s account by conducting a brute force attack, likely due to weak credentials or insufficient account security measures.
## Lateral Movement to Apache Server:
- Using the access gained through user_J, the attackers moved laterally to the Apache server. This may have been achieved through credential reuse, privilege escalation, or exploiting misconfigurations.
## DDoS Attack via POST Requests:
- Once in control of the Apache server, the attackers launched a Distributed Denial-of-Service (DDoS) attack, targeting the /VSI_Account_logon.php endpoint with POST requests to exhaust server resources.
