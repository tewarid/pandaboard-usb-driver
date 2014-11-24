panda_usb_driver
================

This is a test signed Windows driver for PandaBoard. It is just a set of modifications to the Google USB driver that ships with the Android SDK. The product and vendor ID for PandaBoard are documented at http://source.android.com/source/initializing.html under section Configuring USB Access.

Steps to self-sign if you do change the INF. See http://msdn.microsoft.com/en-us/library/windows/hardware/ff546236.aspx for more details. You'll need the Windows Driver Kit. In Windows Driver Kit 7.1, all commands located under bin\amd64 except if indicated otherwise below. In Windows Driver Kit 8.1, all commands are located under bin\x64. 

Execute:

makecert.exe -r -pe -ss PrivateCertStore -n CN=PandaBoard.org(Test) PandaBoard.cer

Inf2cat.exe /driver:. /os:7_x64,7_X86
Note: In Windows Driver Kit 7.1 located under bin\selfsign, and in Windows Driver Kit 8.1 located under bin\x86

Signtool.exe sign /v /s PrivateCertStore /n PandaBoard.org(Test) /t http://timestamp.verisign.com/scripts/timstamp.dll androidwinusba64.cat

Signtool.exe sign /v /s PrivateCertStore /n PandaBoard.org(Test) /t http://timestamp.verisign.com/scripts/timstamp.dll androidwinusb86.cat

certmgr.exe /add PandaBoard.cer /s /r localMachine root
