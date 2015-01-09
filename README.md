# GleSYS API/Ansible Demo. (for Debian 7)

This is an automated procedure to:

  * create a server with provided fqdn.
  * set DNS record for the specified domain.
  * set PTR record to the newly created servers ip.
  * install Wordpress, base install with Ansible (http://docs.ansible.com/)


## Installation.


#### Step 1 – API Key

   * Create a GleSYS API key with IP, DOMAIN and SERVER privilegies. ( `Permissions -> Allow all on  IP, Domain och Server` )
   * use a domain which is maintained on your GleSYS account. (record should not pre-exist)


#### Step 2 - Requirements (where you initiate the script)

   * ansible 1.7
   * sshpass
   * pwgen
   * xmlstarlet
   * curl
   * python passlib library
   * nmap
   * git-core

Below is installation instructions for the requirements on Debian/Ubuntu and MacOS X, however it is possible to keep on using your prefered OS, just find above packages for your OS and you'll be good to go.


###### Install these on Debian/Ubuntu.


	apt-get install python-dev build-essential python-pip pwgen xmlstarlet curl sshpass nmap python-passlib
	pip install ansible 
	git clone https://github.com/GleSYS/wp-auto-deploy.git
	cd wp-auto-deploy
	#edit API credentials in deploy.sh
	./deploy.sh blog.domain.com


###### Install these on MacOS X (using homebrew).


	brew install ansible
	brew install xmlstarlet
	brew install nmap
	brew install pwgen
	brew install https://raw.github.com/eugeneoden/homebrew/eca9de1/Library/Formula/sshpass.rb ( Homebrew doesnt want to merge this https://github.com/Homebrew/homebrew/pull/9577 but its what ansible uses)
	brew install python
	pip install passlib

	
        git clone https://github.com/GleSYS/wp-auto-deploy.git
        cd wp-auto-deploy
        #edit API credentials in deploy.sh
        ./deploy.sh blog.domain.com



#### Step 3 - Run the script.
=====================================

First: Add your API credentials to deploy.sh where it says:


        #Api Credentials
        USER=PLACE_YOUR_ACCOUNT_HERE    #CL12345
        KEY=PLACE_YOUR_KEY_HERE


Then run the script with: (dont forget to check Requirements first)


        ./deploy.sh fqdn (./deploy.sh blog.domain.com)



## This will be installed on the remote host.


   * Debian 7 as template (for this demo, you can edit the ansible playbook  as you like to make it compatible with other dists.)
   * apache2.2
   * MySQL 5.5
   * PHP5.4
   * Postfix (smtp)
   * ProFTPd (ftp server)
   * Latest Wordpress (post-setup config is done with http://wp-cli.org/)


## GleSYS API calls used.

   * Create server (https://github.com/GleSYS/API/wiki/Full-API-Documentation#servercreate)
   * List domain records (https://github.com/GleSYS/API/wiki/Full-API-Documentation#domainlistrecords)
   * Add domain record (https://github.com/GleSYS/API/wiki/Full-API-Documentation#domainaddrecord)
   * Update PTR for ip (https://github.com/GleSYS/API/wiki/Full-API-Documentation#ipsetptr)
