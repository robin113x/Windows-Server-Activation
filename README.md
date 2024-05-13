# Windows Server Activation Guide

This guide provides instructions and scripts for activating Windows Server editions.

## Activation Process

1. **Set Edition and Product Key:**
   Run the following command in Command Prompt (run as administrator) to set the edition to Server Datacenter and provide the product key:
   ```
   dism /online /set-edition:serverdatacenter /productkey:wx4nm-kywyw-qjjr4-xv3qb-6vm33 /accepteula
   ```

2. **Check Current Edition:**
   Verify the current edition using:
   ```
   dism /online /get-currentedition
   ```

3. **Unzip Contents:**
   Unzip the downloaded contents and copy them to `C:\Windows\System32\spp\tokens\skus`.

4. **Fix Errors:**
   Execute the following commands to fix potential errors:
   ```cmd
   cscript.exe %windir%\system32\slmgr.vbs /rilc
   cscript.exe %windir%\system32\slmgr.vbs /upk >nul 2>&1
   cscript.exe %windir%\system32\slmgr.vbs /ckms >nul 2>&1
   cscript.exe %windir%\system32\slmgr.vbs /cpky >nul 2>&1
   cscript.exe %windir%\system32\slmgr.vbs /ipk M7XTQ-FN8P6-TTKYV-9D4CC-J462D
   sc config LicenseManager start= auto & net start LicenseManager
   sc config wuauserv start= auto & net start wuauserv
   clipup -v -o -altto c:\
   ```

5. **Path Issue Resolution:**
   If encountering path issues, use these commands:
   ```cmd
   slmgr /upk
   slmgr.vbs /cpky
   slmgr /ckms
   slmgr.vbs /ckms
   slmgr /skms localhost
   ```

Feel free to contribute to this guide on GitHub.
