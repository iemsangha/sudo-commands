# sudo options and examples

This file lists common `sudo` options, meanings and examples.

## Short options
- `sudo -h` or `sudo --help`  
  Show help text and exit.  
  Example: `sudo --help`

- `sudo -V`  
  Show sudo version information.  
  Example: `sudo -V`

- `sudo -v`  
  Validate/refresh your cached credentials (extend the timeout).  
  Example: `sudo -v`

- `sudo -k`  
  Invalidate the user's timestamp (next sudo will ask for password).  
  Example: `sudo -k`

- `sudo -K`  
  Remove the user's cached credentials completely.  
  Example: `sudo -K`

- `sudo -n`  
  Non-interactive: fail instead of prompting for a password.  
  Example: `sudo -n apt update` (will fail if password required)

- `sudo -u <user>`  
  Run the command as specified user (default is root).  
  Example: `sudo -u www-data systemctl restart nginx`

- `sudo -s`  
  Run a shell as root (preserving environment).  
  Example: `sudo -s`

- `sudo -i`  
  Run login shell as target user (initializes login environment).  
  Example: `sudo -i`

- `sudo -H`  
  Set HOME to the target user's home directory.  
  Example: `sudo -H -u someuser bash -c 'echo $HOME'`

- `sudo -l`  
  List the commands the invoking user is allowed to run (and which require password).  
  Example: `sudo -l`

- `sudo --`  
  End of `sudo` options; following args are the command.  
  Example: `sudo -- ls --color=auto`

## Useful combinations / tips
- Run a single command as another user:
  `sudo -u username command`

- Get a root interactive shell:
  `sudo -i` or `sudo -s`

- Run without password (if you have NOPASSWD in sudoers): `sudo -n command`

## Where to get more details
- `man sudo` — full manual
- `/etc/sudoers` and files under `/etc/sudoers.d/` — configuration for privileges

sudo apt update
sudo apt install nginx
2. Run a command as another user
bash
Copy code
sudo -u <username> <command>
Example:

bash
Copy code
sudo -u www-data ls /var/www
3. Get a root shell
bash
Copy code
sudo -s
Gives you a root shell using your current environment.

4. Get a login root shell
bash
Copy code
sudo -i
Simulates logging in as root (root environment variables apply).

5. Show what sudo allows you to run
bash
Copy code
sudo -l
6. Refresh your sudo timestamp (avoid password re-entry)
bash
Copy code
sudo -v
7. Make sudo ask for password next time
bash
Copy code
sudo -k
8. Run sudo without password prompt (fails if password needed)
bash
Copy code
sudo -n <command>
9. Clear sudo cached credentials completely
bash
Copy code
sudo -K
10. Stop sudo from parsing options
bash
Copy code
sudo -- <command>
Useful when running commands that start with dashes:

bash
Copy code
sudo -- ls -la
Practical Everyday Sudo Use Cases
11. Edit system files that require root
bash
Copy code
sudo nano /etc/hosts
sudo nano /etc/nginx/nginx.conf
12. Restart system services
bash
Copy code
sudo systemctl restart nginx
sudo systemctl restart ssh
13. View logs that require root access
bash
Copy code
sudo journalctl -u nginx
sudo journalctl -xe
14. Change file ownership and permissions
bash
Copy code
sudo chown user:user file
sudo chmod 755 folder
15. Update system packages (Ubuntu/Debian)
bash
Copy code
sudo apt update && sudo apt upgrade -y
16. Run root scripts
bash
Copy code
sudo bash script.sh
Commands Beginners Should Avoid (Dangerous)
❌ Avoid: long root sessions
bash
Copy code
sudo -s
sudo -i
Use only when needed. Always run:

bash
Copy code
exit
to return to normal user.

❌ Avoid: recursive chmod/chown on system directories
bash
Copy code
sudo chmod -R 777 /
sudo chown -R user:user /
This can break your entire OS.

❌ Avoid: editing /etc/sudoers with normal editor
Bad:

bash
Copy code
sudo nano /etc/sudoers
Correct:

nginx
Copy code
sudo visudo
❌ Avoid: piping random internet scripts into root
Bad:

bash
Copy code
curl https://randomsite/install.sh | sudo bash
This can fully compromise your system.


