# WSL
Managemente actions and general notes on Windows Subsystem for Linux

## Integrate WSL with X11 server to support GUI applications 
Motivation:   
Connecting to a X11 server is essential to allow WSL to run GUI applications. 

How: 
1. First, we need to have a X11 server installed. I've chosen [VcXsrv](https://sourceforge.net/projects/vcxsrv/). After following the installation, we need to locate the program in our local machine and Launch it (there may be a `XLaunch` icon in the installation directory). When launching it, select `Multiple windows` > `Start no client` and then make sure you select the `Disable access control` option. 
2. Set the DISPLAY environment variable. First find out your IP: `cat /etc/resolv.conf`. Then export the variable in the ~/.bashrc file: `export DISPLAY=<IP-address>:0`. See more details in [this](https://github.com/microsoft/WSL/issues/4106) github issue (benhillis' answer).
3. Add a separate inbound rule for TCP port 6000 in Windows Defender Firewall (as suggested by [whme's answer](https://stackoverflow.com/questions/61110603/how-to-set-up-working-x11-forwarding-on-wsl2) in StackOverFlow). The steps to set a new inbound rule are described at Microsoft's [official docs](https://docs.microsoft.com/pt-br/windows/security/threat-protection/windows-firewall/create-an-inbound-port-rule).
4. Check that the integration is working by running a GUI app, e.g., *gedit*: `gedit ~/.bashrc`
