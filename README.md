# Automatic Deployment of Masternode 

Ansible Deployment of Masternode (Currently for Ubuntu 16:04)

### Setup Masternode Server
1. Setup VPS with Ubuntu: 16:04
2. Login to server
3. Run the following commands
    -  sudo apt-get update -y
   -   sudo apt-get install -y ansible git
   -   git clone https://github.com/vivocoin/ansible.git
    -  cd ansible/
    -  vi deployment.yaml enter in ip-address (i.e. 257.257.257.257:12845)
     - replace "{{ ipaddr }}" with the current ip-address. i.e. my_ipaddr: "{{ ipaddr }}" ---> my_ipaddr: 257.257.257.257:12845
  -    exit out of vi
4. Run the playbook
     - sudo ansible-playbook deployment.yaml
    -  wait 50 minutes
    -  copy the output for the masternode key value i.e. 7edfdewd3wvZi6JQfewwefr32qeymkB2G4ebXhch
5. Insert the crontab
    -  crontab -e
    -  \* * * * * cd /home/YOURUSERNAME/.vivocore/sentinel && ./venv/bin/python bin/sentinel.py 2>&1 >> sentinel-cron.log
6. Reboot the Ubuntu Machine by running the following command
    -  sudo reboot
7. Login to the server
8. CD to /vivo_ubuntu16.04_3_wwf/
     - cd /vivo_ubuntu16.04_3_wwf/
9. Run the following command
   -   ./vivo-cli start
10. Wait for the masternode to connect
11. Check masternode status
    -  ./vivo-cli masternode status


### Local Machine - Masternode settings 
-------

Masternode.conf Template <br/>
*********** <br/>
Label: \<INSERT in name of masternode label> <br/>
Collateral address: \<INSERT in collateral address> <br/>
Masternode Key: \<INSERT masternode key value> <br/>
Public IP: \<INSERT public ip address>:12845 <br/>
MN conf line: \<INSERT in conf line> <br/>
*********** <br/>

----

1. On local machine -- open up local wallet
2. click receive
3. type in label name: MN1
     - this value goes into the Label: 
4. uncheck instant send
5. click request payment
6. copy the address value VQVdsfg34trfswfx8gqJ4AyifwSuFzNHs
    -  this value goes into the Collateral address: 
8. send exactly 1000 VIVO to the collateral address
9. goto console (Tools --> debug console): Enter in
     - masternode outputs
10. copy the output “c89f1d48efe79df79698sdf98sdf98ds63cd6edeabcd2d5e1d7e97bbb70d”: “1” in without quotes
     - this value goes into the MN conf line: c89f1d48efe79df79698sdf98sdf98ds63cd6edeabcd2d5e1d7e97bbb70d 1
11. Copy the masternode key output from the ansible script 
    -  this value goes into the masternode key: 7edfdewd3wvZi6JQfewwefr32qeymkB2G4ebXhch
    - this value can also be seen with "sudo cat /root/.vivocore/vivo.conf"
12. Copy the ip address into the Public IP

*********** <br/>
Label: MN1 <br/>
Collateral address: VQVdsfg34trfswfx8gqJ4AyifwSuFzNHs <br/>
Masternode Key: 7edfdewd3wvZi6JQfewwefr32qeymkB2G4ebXhch <br/>
Public IP: 257.257.257.257:12845 <br/>
MN conf line: c89f1d48efe79df79698sdf98sdf98ds63cd6edeabcd2d5e1d7e97bbb70d 1 <br/>
*********** <br/>


#### Windows Wallet - Masternode.conf location
Windows --- Edit this file
C:\Users\ \<username>\AppData\Roaming\VivoCore\masternode.conf

#### Mac Wallet - Masternode.conf location
Mac
edit /Users/\<username>/Library/Application\ Support/VivoCore/masternode.conf

#### Edit the Masternode.conf file
under 
"# Masternode config file"
"# Format: alias IP:port masternodeprivkey collateral_output_txid collateral_output_index"

paste in the following:
MN1 257.257.257.257:12845 7edfdewd3wvZi6JQfewwefr32qeymkB2G4ebXhch c89f1d48efe79df79698sdf98sdf98ds63cd6edeabcd2d5e1d7e97bbb70d 1

Save the file
open up vivo-qt (vivo wallet) --> settings --> options --> wallet tab
Show Masternode tab
Restart vivo-qt

click masternodes tab
select MN1 alias
click start alias

#### Masternode should now be deployed
