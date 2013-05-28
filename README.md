panda_usb_driver
================

This is a test signed Windows driver for PandaBoard. It is just a modified Google USB driver that ships with the Android SDK. The product and vendor ID for PandaBoard are documented at http://source.android.com/source/initializing.html under section Configuring USB Access.

Steps to self-sign if you do change the INF [http://msdn.microsoft.com/en-us/library/windows/hardware/ff546236.aspx]. You'll need the Windows Driver Kit.

"C:\Program Files (x86)\Windows Kits\8.0\bin\x64\makecert.exe" -r -pe -ss PrivateCertStore -n CN=PandaBoard.org(Test) PandaBoard.cer

"C:\Program Files (x86)\Windows Kits\8.0\bin\x64\Inf2cat.exe" /driver:. /os:7_x64,7_X86

"C:\Program Files (x86)\Windows Kits\8.0\bin\x86\Signtool.exe" sign /v /s PrivateCertStore /n PandaBoard.org(Test) /t http://timestamp.verisign.com/scripts/timstamp.dll androidwinusba64.cat

"C:\Program Files (x86)\Windows Kits\8.0\bin\x86\Signtool.exe" sign /v /s PrivateCertStore /n PandaBoard.org(Test) /t http://timestamp.verisign.com/scripts/timstamp.dll androidwinusb86.cat

"C:\Program Files (x86)\Windows Kits\8.0\bin\x64\certmgr.exe" /add PandaBoard.cer /s /r localMachine root
