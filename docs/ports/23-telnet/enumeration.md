RustScan Practical

Objective
To perform a network port scan on the target machine using RustScan and identify all open TCP ports and the services running on them.

Lab Setup
Machine	IP Address
Kali Linux	<Attacker IP>
Target Machine	<Target IP>
Step 1: Verify Network Connectivity

Before performing the scan, I verified that the target machine was reachable from the Kali Linux system.

Command
ping <Target IP>

Output:
<img width="831" height="202" alt="Screenshot 2026-07-10 141220" src="https://github.com/user-attachments/assets/63e1fd50-2054-4167-ad49-874cf52547b8" />


Step 2: Perform RustScan

After verifying connectivity, I executed RustScan against the target machine.

Command
rustscan -a <Target IP>

RustScan performed a fast TCP port scan and automatically launched Nmap to enumerate the discovered services.

Output:

<img width="540" height="827" alt="image" src="https://github.com/user-attachments/assets/906562d8-89c7-4029-b040-c0766689344c" />
<img width="487" height="557" alt="image" src="https://github.com/user-attachments/assets/33305986-22bc-4fd9-993f-2f08a934f97c" />


Step 3: Open Ports Identified

The following open TCP ports were identified during the scan.

Port	Service	Status
21	FTP	Open
22	SSH	Open
23	Telnet	Open
25	SMTP	Open
53	DNS	Open
80	HTTP	Open
111	RPCBind	Open
139	NetBIOS	Open
445	SMB	Open
512	Remote Exec	Open
513	Rlogin	Open
514	RSH	Open
1099	Java RMI	Open
1524	Ingreslock	Open
2049	NFS	Open
2121	FTP	Open
3306	MySQL	Open
3632	DistCCD	Open
5432	PostgreSQL	Open
5900	VNC	Open
6000	X11	Open
6667	IRC	Open
6697	IRCS	Open
8009	AJP13	Open
8180	HTTP	Open
8787	Message Server	Open
47204	Unknown	Open
52657	Unknown	Open
55686	Unknown	Open
56140	Unknown	Open
Step 4: Service Version Detection

To identify the versions of the running services, I performed version detection using RustScan with Nmap.

Command
rustscan -a <Target IP> -- -sV

Output:

<img width="932" height="585" alt="image" src="https://github.com/user-attachments/assets/42fc375c-502c-4270-9ed7-d8f86e89171c" />


Step 5: Default Script Scan

Next, I executed the default Nmap scripts together with service version detection.

Command
rustscan -a <Target IP> -- -sC -sV

Output:
<img width="951" height="821" alt="image" src="https://github.com/user-attachments/assets/51591885-9d2b-47cf-a6f8-8e63b02b2c82" />
<img width="947" height="812" alt="image" src="https://github.com/user-attachments/assets/f3a43000-9522-4b93-9747-d1c7d94e1d59" />

Step 6: Aggressive Scan

To gather additional information such as operating system details, service information, and default NSE script results, I performed an aggressive scan.

Command
rustscan -a <Target IP> -- -A

Output:
<img width="948" height="845" alt="image" src="https://github.com/user-attachments/assets/d52b1ad5-bb2e-4a1f-ad2a-283b197514af" />
<img width="946" height="818" alt="image" src="https://github.com/user-attachments/assets/7e4c88b9-680a-4f9e-a4d2-8918c660c62c" />


Step 7: Save the Scan Results

The scan results were saved into a text file for documentation and future reference.

Command
rustscan -a <Target IP> -- -A > rustscan_report.txt

To verify the saved report:

cat rustscan_report.txt

Scan Summary

The RustScan scan successfully identified multiple open TCP ports on the target machine. The scan also integrated with Nmap to enumerate the corresponding network services. Based on the scan results, several services such as FTP, SSH, Telnet, SMTP, HTTP, SMB, MySQL, PostgreSQL, VNC, Apache Tomcat, and other network services were found to be running on the target system.

The information gathered during this reconnaissance phase can be used for further authorized security assessment and service analysis.

Commands Used
ping <Target IP>

rustscan -a <Target IP>

rustscan -a <Target IP> -- -sV

rustscan -a <Target IP> -- -sC -sV

rustscan -a <Target IP> -- -A

rustscan -a <Target IP> -- -A > rustscan_report.txt

cat rustscan_report.txt
