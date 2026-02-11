# FiservDNA ACS Installation

Download the ACS FiservDNA software from the SMA FTP Site.
Location will be in
**/OpCon Releases/Integrations/FiservDNA/** 
Select the required version.

- Unzip the FiservDNA.zip file.
- On-prem customers 
  Copy the FiservDNA directory to the \\SAM\\plugins directory
  Restart the **SMA OpCon Services Manager** and **SMA OpCon RestAPI** service.
- Cloud customers
  Copy the FiservDNA directory to the \\Relay\\plugins directory
  Restart the **SMA OpCon Relay** service.

# FiservDNA ACS Upgrade

Download the ACS FiservDNA selected software upgrade from the SMA FTP Site.
Location will be in
**/OpCon Releases/Integrations/FiservDNA/** 

- Unzip the FiservDNA.zip file.
- On-prem customers 
  Stop the **SMA OpCon Services Manager** and **SMA OpCon RestAPI** service.
  Copy the FiservDNA directory to the \\SAM\\plugins directory
  Restart the **SMA OpCon Services Manager** and **SMA OpCon RestAPI** service.
- Cloud customers
  Stop the **SMA OpCon Relay** service.
  Copy the FiservDNA directory to the \\Relay\\plugins directory
  Restart the **SMA OpCon Relay** service.