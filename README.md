# Local-privilege-escalation-scenarios

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
Sure, let's provide more technical detail for these use cases:

14. **Insecure NFS Exports:** Use `showmount -e <ip address>` to list NFS shares. Look for shares that are exported to "*", and test if you can mount them and write files. 

15. **Abusing sudo Rights with Wildcards:** Check the sudo configuration with `sudo -l`. Look for commands that include the wildcard character (*) and try replacing the * with a symlink to a different file.

16. **Running Processes:** Use the `lsof` command to list open files and the processes that opened them. Look for files that are owned by a higher-privilege user but are accessible by a lower-privilege process. If possible, try reading from these files.

17. **LD_PRELOAD Exploits:** Check environment variables of running processes. This can sometimes be done with commands like `ps eww <PID>`, where `<PID>` is the Process ID. If the LD_PRELOAD environment variable is set, research the library it's loading to see if it can be exploited.

18. **Privilege Escalation via CAP_SETUID:** Check the capabilities of running processes using the `getpcaps <PID>` command. If a process has the CAP_SETUID capability, this could potentially be used for privilege escalation. 

19. **Exploiting Setuid-root Binaries:** Find all SUID root binaries with the command `find / -user root -perm -4000 -print 2>/dev/null`. Research these binaries to see if they have any known vulnerabilities, or use a fuzzer to test them for vulnerabilities.


