# Troubleshooting Log - First VM setup

| Machine          | OS           | Total Physical Memory |Purpose                                 |
|------------------|--------------|-----------------------|----------------------------------------|
| VirtualBox-7.2.8 | Ubuntu 22.04 | 7.69 GB               |To set up a functional Home-lab set-up. |

All commands were told to me by CLAUDE AI, since, as a beginner, I had no prior experience or knowledge of the required
commands.
## Problem_01: Not enough RAM
While installing Ubuntu-22.04, I found that I had only 579MB RAM available, while Windows consumed most of it actively. This much was not enough for a VM to function properly.
### What I tried:
- I checked active memory usage in Task Manager and explored details about my system in System Information. Surprisingly, Chrome was using most of the RAM, nearly 500MB, even when I had 1 active tab (CLAUDE) open.
- I researched 'why is my laptop not having enough RAM?' A common reason is the pre-installation of bloatware. It included antivirus apps and a gaming setup with an Xbox. I deleted these upon finding them. This freed 3.12 GB RAM, out of which I allocated 2 GB RAM to the VM.
### What I learnt:
- Chrome is infamous for using a large amount of RAM for background processes (equivalent to 23 open tabs). Thus, while using VM, no Chrome window should be open. Microsoft Edge is a good alternative.
- Upon buying new devices, and for future uses, delete bloatware first and foremost for more productivity.
## Problem_02: Guest Addition
 - I ran the command ' sudo apt install -y gcc make perl ' to download and install the build tools needed for guest additions. But it showed that the packages were too old.
 - It connected but failed to reach Ubuntu's servers, - DNS/network routing issue in the VM.
 - Ubuntu's default Indian mirror was blocking connections on port 80 (HTTP).
 - It was continuously failing, "gcc-12:not found".
 ### What I tried:
 - I ran the command ' sudo apt update ' to update the packages.
 - I ran the command ' ping -c 3 8.8.8.8 ' to check if the basic network works.
 - I ran the command ' echo "nameserver 8.8.8.8" | sudo tee /etc/resolv.conf ' to resolve the DNS error.
 - I switched to HTTPS mirrors.
 - I ran the command ' sudo apt install -y gcc-12 ' as it turns out, gcc-11.4 was too old for Guest Additions.
 ### What I learnt:
 - ' sudo apt update ' command refreshes the package list.
 - ' ping -c 3 8.8.8.8 ' command checks basic network working. If it shows "0% packet loss", the basic network is there.
 - ' echo "nameserver 8.8.8.8" | sudo tee /etc/resolv.conf ' corrects the DNS error if it shows " nameserver 8.8.8.8 " by overwriting old, broken or outdated files with a manual DNS address. 
 - ' sudo apt install -y gcc-12 ' command installs the gcc-12.
 - ' sudo reboot ' command reboots the VM.
## Problem_03: Password Change
I exposed my password to the terminal by entering it after incorrectly entering the command ' sudo apt update '.
### What I tried:
I ran the command ' passwd ' to change my password by entering my old password, entering and confirming the new password. 
### What I learnt:
' passwd ' command is used to update passwords.
