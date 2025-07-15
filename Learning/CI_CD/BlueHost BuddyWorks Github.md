#CI/CD #linux #shell #ssh #github 
- Creating host SSH key in cPanel
	- Name: `id_rsa_bluehost` 
	- Key password: `4t2E3-1RQ[Hu`
- Manage key → Authorize
- Click view `id_rsa_bluehost.pub` key and copy public key
- Add this `.pub` key to GitHub `Settings` -> `SSH and GPG keys`
- Add this `.pub` key to BuddyWorks profile(your BuddyWorks account password)![[Pasted image 20230827193246.png]]
- Go to the server trough terminal using SSH credentials
	- Add private SSH key to an SSH agent using `ssh-add ~/.ssh/id_rsa_bluehost
		- If `UNPROTECTED KEY` error, run this to make sure both keys are protected:
		  `chmod 600 /home3/avwyiumy/.ssh/id_rsa_bluehost.pub`
		  `chmod 600 /home3/avwyiumy/.ssh/id_rsa_bluehost`
		  Replace `/home3/avwyiumy/` with your server path
		  Replace `id_rsa_bluehost` with your key
	- If SSH agent is not running, activate it first with `eval "$(ssh-agent -s)"`
	- Check if key is added with `ssh-add -l`
- Go to server terminal using SSH credentials and set up git on the server
	- `git init`
	- `git remote add git@github.com:guidance/Skin-Center.git`
- Then create BuddyWorks pipeline and call it "Deploy to PROD" or "Deploy to STAGE"
- Add an action "SSH"![[Pasted image 20230827183230.png]]
- In "Run CMDs" tab add `git pull origin master`![[Pasted image 20230827183336.png]]
- In "Target" tab add your information (SSH credentials and server path):
	- Hostname (in this case - `avw.yiu.mybluehost.me`)
	- Login (in this case - `avwyiumy`)
	- Use "Custom private key" and an authentication option
	- Add private key that you can download from cPanel (Private, NOT the .pub version)
	- SSH key passphrase (The one you used when creating an SSH key on a server)
	- Working directory (in this case - `public_html/.website_baaf6c32/wp-content`)
- Tabs "Variables", "Conditions" and "Options" you can leave as default
- 