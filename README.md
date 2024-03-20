#Active Directory Pentest
Components:

	![Capture](https://github.com/Anub1s1999/WindowsExecutables/assets/91386350/1039ece9-48a7-4028-903d-831b1a31ee91)

Detections:

	![Capture_Detections](https://github.com/Anub1s1999/WindowsExecutables/assets/91386350/80f90de4-7467-4a32-8fc9-5aa46e8943fb)

Bypassing Execution Policy:
	
 	*It is NOT a security measure, it is present to prevent user from 
		accidently executing scripts.
 	*Several ways to bypass
		powershell –ExecutionPolicy bypass
		powershell –c <cmd>   ////Only Commands
		powershell –encodedcommand
		$env:PSExecutionPolicyPreference="bypass"
Bypassing PowerShell Security:
	
 	use Invisi-Shell (https://github.com/OmerYa/Invisi-Shell) for bypassing the security controls in PowerShell.
	The tool hooks the .NET assemblies (System.Management.Automation.dll and System.Core.dll) to bypass logging
	It uses a CLR Profiler API to perform the hook.
	"A common language runtime (CLR) profiler is a dynamic link library (DLL) that consists of functions that receive messages from, and send messages to, the CLR by using the profiling API. The profiler DLL is loaded by the CLR at run time."
Bypassing AV Signatures for PowerShell:
	
 	*load scripts in memory and avoid detection using AMSI bypass.
	How do we bypass signature based detection of on-disk PowerShell scripts by Windows Defender?
		We can use the AMSITrigger (https://github.com/RythmStick/AMSITrigger) tool to identify the exact part of a script that is detected.
	Simply provide path to the script file to scan it:
		AmsiTrigger_x64.exe -i <"Path To The Script for testing it">
	*For full obfuscation of PowerShell scripts, see Invoke-Obfuscation (https://github.com/danielbohannon/Invoke-Obfuscation). That is used for obfuscating the AMSI bypass in the course!
 ![Example-BypassingAV](https://github.com/Anub1s1999/WindowsExecutables/assets/91386350/814cdce0-f2aa-4f65-b56e-8111ea86f84f)

	
