# Local-privilege-escalation-scenarios

privilege escalation scenarios


1. **Sudo Privileges:** Check which commands the current user can run as sudo using the command `sudo -l`.

2. **Misconfigured SUID and SGID Files:** Find all SUID files using `find / -perm -u=s -type f 2>/dev/null` and all SGID files using `find / -perm -g=s -type f 2>/dev/null`.

3. **Kernel Exploits:** Keep the kernel up-to-date and use tools like Lynis for more thorough checks.

4. **Weak File Permissions:** Find world-writable files using `find / -type f -perm -2 ! -user root -ls 2>/dev/null`.

5. **Software Bugs:** Keep all software updated and run with the least privileges necessary. Use vulnerability scanners like Nessus, OpenVAS, or Nikto.

6. **Unsecured Service Configurations:** Check configurations for all running services to ensure they don't grant excessive permissions or expose sensitive information.

7. **Cron Jobs:** Look at all cron jobs (which can typically be found in /etc/crontab or /etc/cron.* directories) for any that run scripts or executables with weak permissions.

8. **Poorly Secured PATH Variables:** Check the PATH for all users, especially privileged users, to ensure there are no writable directories before important system directories. The command `echo $PATH | tr ':' '\n'` will list the directories in the PATH.

9. **Buffer Overflows:** Keep all software up-to-date and consider using security features like address space layout randomization (ASLR) that can help mitigate the impact of buffer overflows.

10. **Race Conditions:** This is harder to test for, but be wary of high-privilege processes that depend on the timing of other processes.

11. **Service Exploits:** Keep all services up-to-date and disable unnecessary ones. Use vulnerability scanners to check for known vulnerabilities in your services.

12. **Unintentional Exposure of Credentials:** Regularly audit your system for exposed credentials. Be careful with commands like `ps` that might expose command-line arguments, and avoid hard-coding passwords or keys in your scripts or programs.

13. **Docker Misconfigurations:** If Docker is used, understand the security implications. Be wary of adding users to the docker group, as this gives them the potential to gain root access.

