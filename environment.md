# Environment

[HypriotOS 1.9.0](https://blog.hypriot.com/downloads/):

* SSH server enabled out of the box
* Default credentials: `pirate` / `hypriot`

Run on any host:

```
$ uname -a
```

Output:

```
Linux master 4.14.34-hypriotos-v7+ #1 SMP Sun Apr 22 14:57:31 UTC 2018 armv7l GNU/Linux
```

Run on any host:

```
$ cat /etc/os-release
```

Output:

```
PRETTY_NAME="Raspbian GNU/Linux 9 (stretch)"
NAME="Raspbian GNU/Linux"
VERSION_ID="9"
VERSION="9 (stretch)"
ID=raspbian
ID_LIKE=debian
HOME_URL="http://www.raspbian.org/"
SUPPORT_URL="http://www.raspbian.org/RaspbianForums"
BUG_REPORT_URL="http://www.raspbian.org/RaspbianBugs"
```

Run on any host:

```
$ docker version
```

Output:

```
Client:
 Version:       18.04.0-ce
 API version:   1.37
 Go version:    go1.9.4
 Git commit:    3d479c0
 Built: Tue Apr 10 18:25:24 2018
 OS/Arch:       linux/arm
 Experimental:  false
 Orchestrator:  swarm

Server:
 Engine:
  Version:      18.04.0-ce
  API version:  1.37 (minimum version 1.12)
  Go version:   go1.9.4
  Git commit:   3d479c0
  Built:        Tue Apr 10 18:21:25 2018
  OS/Arch:      linux/arm
  Experimental: false
```

Run on all hosts:

```
$ sudo timedatectl set-timezone Europe/Moscow
```
