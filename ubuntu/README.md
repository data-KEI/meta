### 설치 후 해야할 것!!!
- 대기모드 비활성화: sudo systemctl mask sleep.target suspend.target hibernate.target hybrid-sleep.target
~~~
$ sudo systemctl status sleep.target
[sudo] password for user:
○ sleep.target - Sleep
     Loaded: loaded (/lib/systemd/system/sleep.target; static)
     Active: inactive (dead) since Tue 2022-09-27 00:02:28 UTC; 5min ago
       Docs: man:systemd.special(7)

Sep 26 07:10:12 keimeta systemd[1]: Reached target Sleep.
Sep 27 00:02:28 keimeta systemd[1]: Stopped target Sleep.
$ sudo systemctl status suspend.target
○ suspend.target - Suspend
     Loaded: loaded (/lib/systemd/system/suspend.target; static)
     Active: inactive (dead)
       Docs: man:systemd.special(7)

Sep 27 00:02:28 keimeta systemd[1]: Reached target Suspend.
Sep 27 00:02:28 keimeta systemd[1]: Stopped target Suspend.
$ sudo systemctl status hibernate.target
○ hibernate.target - System Hibernation
     Loaded: loaded (/lib/systemd/system/hibernate.target; static)
     Active: inactive (dead)
       Docs: man:systemd.special(7)
$ sudo systemctl status hybrid-sleep.target
○ hybrid-sleep.target - Hybrid Suspend+Hibernate
     Loaded: loaded (/lib/systemd/system/hybrid-sleep.target; static)
     Active: inactive (dead)
       Docs: man:systemd.special(7)
$ sudo systemctl mask sleep.target suspend.target hibernate.target hybrid-sleep.target
Created symlink /etc/systemd/system/sleep.target → /dev/null.
Created symlink /etc/systemd/system/suspend.target → /dev/null.
Created symlink /etc/systemd/system/hibernate.target → /dev/null.
Created symlink /etc/systemd/system/hybrid-sleep.target → /dev/null.
$ sudo systemctl status sleep.target
○ sleep.target
     Loaded: masked (Reason: Unit sleep.target is masked.)
     Active: inactive (dead) since Tue 2022-09-27 00:02:28 UTC; 8min ago

Sep 26 07:10:12 keimeta systemd[1]: Reached target Sleep.
Sep 27 00:02:28 keimeta systemd[1]: Stopped target Sleep.
~~~
