#Active Directory Pentest
Components:
	
Detections:
	
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
	
