- The user named "root"/superuser/admin is a special user in UNIX-like OS that has unrestricted/full read, write and execute privileges to all areas of the filesystem.
- We should not log in as the root user unless required.
	- Disabling root login is a safe practice against hacker/virus.
	- Preventing mistakes while working. You can do everything as superuser, and the system won't ask. One click format will wipe out every of your data.
	- Limit damage of security vulnerability. Applications are meant to be run with non-admin security (user/mortal level) and all administrative tasks are for the root user on a per-need basis. By logging in the root user, you are running all applications with root privileges.
	- Accountability -> who is responsible for which.
## How to block root login
1. Login to root account?
2. Switch to another pre-created account with sudo privileges. -> `su noah`.
3. [4 Ways to Disable Root Account in Linux (tecmint.com)](https://www.tecmint.com/disable-root-login-in-linux/#:~:text=The%20simplest%20method%20to%20disable,command%20line%20editors%20as%20shown.&text=Save%20the%20file%20and%20close%20it.)