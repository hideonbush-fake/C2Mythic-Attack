# C2Mythic-Attack-and-Detect

## Objective


### Attack Diagram
![2025-03-07 10_48_45-Untitled Diagram drawio - draw io](https://github.com/user-attachments/assets/bb02f68d-69bf-49dc-89d6-c5045c9741ea)
![2025-03-07 10_49_01-Untitled Diagram drawio - draw io](https://github.com/user-attachments/assets/7f936758-e35f-4d7d-ad4e-ed35d2240456)

#### Skills Learned

## Attack Phases
### PHASE 0 (SETUP)
- SSH into Mythic Server & apt install and enable docker-compose (Mythic is a containerized system --> Docker services manage and run C2 efficiently)
- Gitclone: "https://github.com/its-a-feature/Mythic"
- Start the Mythic-CLI

![2025-03-07 10_52_43-root@MYTHIC-SERVER_ ~_Mythic](https://github.com/user-attachments/assets/85c4f311-5d57-4ecb-afa1-4734fc85a088)
![2025-03-07 10_53_25-root@MYTHIC-SERVER_ ~_Mythic](https://github.com/user-attachments/assets/77b6c085-d0bb-4d18-86c7-71b723650764)
![2025-03-07 10_54_45-root@MYTHIC-SERVER_ ~_Mythic](https://github.com/user-attachments/assets/eee37928-f1ff-4fa9-8431-8a95e17b5033)

- Create a password file on the Windows Server containing the current password (Winter2025!), as it is a commonly used password
- Use the rockyou.txt wordlist sample in the Kali VM, edit the file, and add Winter2025! to the list

![2025-03-07 11_06_20-155 138 163 229 - Remote Desktop Connection](https://github.com/user-attachments/assets/0705051a-aa61-4e4c-b1be-00abca56e28d)
![Screenshot 2025-03-07 110739](https://github.com/user-attachments/assets/837de843-3dbd-408e-aab0-434463d2085e)
![Screenshot 2025-03-07 110750](https://github.com/user-attachments/assets/a6aad53d-2e95-41c5-88c4-aa9e0828d05b)

### PHASE 1 (INITIAL ACCESS)
- Download Crowbar in Kali VM to perform RDP brute force attack with the "mythicwordlist"

![Screenshot 2025-03-07 111139](https://github.com/user-attachments/assets/669852a8-f441-4cd8-9490-f333ba501407)

- After a successful RDP brute force, we have the following credentials "Administrator:Winter2025!"

![Screenshot 2025-03-07 111348](https://github.com/user-attachments/assets/50d86c00-4d35-48e7-808a-bae0230b15e8)

### PHASE 2 (DISCOVERY)
- Use XFREERDP to establish an RDP connection and authenticate into the system, then execute commands to gather reconnaissance on the account

![Screenshot 2025-03-07 111456](https://github.com/user-attachments/assets/da307222-d32f-498a-9f6a-f726f6f76327)

### PHASE 3 (DEFENSE EVASION)
- Use CMD to disable Window Defender

![Screenshot 2025-03-07 111620](https://github.com/user-attachments/assets/14045543-9d03-4b68-8d9e-9a3728d862e0)

### PHASE 4 (EXECUTION)
- Download C2 Agent on to the Mythic Server "https://github.com/MythicAgents/Apollo"
- Download C2 Profile "https://github.com/MythicC2Profiles/http"
- Create a payload on Mythic Web Gui & download it to our Mythic Server
- Create a new filename

![2025-03-07 13_47_36-Mythic](https://github.com/user-attachments/assets/407932ec-7d5d-47b7-bc4a-70227fd1401e)
![2025-03-07 13_48_47-root@MYTHIC-SERVER_ ~_MalPayload](https://github.com/user-attachments/assets/357d1ac3-530d-40e1-ac9d-34159c09d706)

- Use Python's built-in HTTP module to host and deliver a malicious payload to the victim's system
  
![2025-03-07 13_50_03-root@MYTHIC-SERVER_ ~_MalPayload](https://github.com/user-attachments/assets/60a5a974-fd61-4a72-b355-841132fbcecc)

- Return to the XFREERDP session from Phase 2 and use Invoke-WebRequest in PowerShell.
- Execute the malicious payload to establish a C2 connection with the Mythic Web GUI.

![Screenshot 2025-03-07 140953](https://github.com/user-attachments/assets/e35e26bf-7c4e-4aa2-9c3d-b05c9e332749)
![Screenshot 2025-03-07 141033](https://github.com/user-attachments/assets/91493243-3ee4-4ead-a09f-2e3e851f7a01)

### PHASE 5/6 (EXECUTION $ EXFILTRATION)
- Successfully established a C2 connection with the Mythic Web GUI, able to run commands

![2025-03-07 14_39_18-Mythic](https://github.com/user-attachments/assets/42a483e8-7422-4e68-aa55-24401086ca8e)

- EXFIL w/this command: download C:\Users\Administrator\Documents\password

![2025-03-07 14_47_05-Mythic](https://github.com/user-attachments/assets/5f12955b-a6b9-4e7e-9cb8-670d78aa6a21)





























