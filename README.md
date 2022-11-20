<div align=center>
  <h1>
    <img src="immutablefs.png"/>
    <br>immutablefs
  </h1>
  <i>An simple and easy-to-use on-demand immutability based on file attributes.</i>
</div>

# What is?

It is a mechanism to leave key parts of the system non-writable while others remain writable with a high level of granularity, with this method it is possible for e.g. allow files in `/etc` to be modifiable but at the same time block the creation of new files or removal of existing files em `/etc`

# How its works?

 This works by calling `chattr +i` where it should be read-only and `chattr -i` where it should be writable, the places are defined through "modes" currently the software has 3 modes, the modes and places are described below:
 🔓🔒📝
 | Path | strict | basic | classic |
 |------------------|--------|-------|---------|
 | /etc             | ❌     | 📝    | ✔️       |
 | /usr             | ❌     | ❌    | ❌      |
 | /var             | ❌     | ❌    | ✔️      |
 | /lib             | ❌     | ❌    | ❌      |
 | /lib64           | ❌     | ❌    | ❌      |
 | /lib32           | ❌     | ❌    | ❌      |
 | /bin             | ❌     | ❌    | ❌      |
 | /sbin            | ❌     | ❌    | ❌      |
 | /var/lib/flatpak | ✔️     | ✔️    | ✔️      |
 | /var/lib/snapd   | ✔️     | ✔️    | ✔️      |
 | /var/logs        | ✔️     | ✔️    | ✔️      |
 | /var/cache       | ✔️     | ✔️    | ✔️      |
 | /var/tmp         | ✔️     | ✔️    | ✔️      |
 | /var/www         | ✔️     | ✔️    | ✔️      |
 | /etc/mtab        | 📝     | 📝    | ✔️      |
 | /etc/group       | 📝     | 📝    | ✔️      |
 | /etc/passwd      | 📝     | 📝    | ✔️      |
 | /etc/shadow      | 📝     | 📝    | ✔️      |
 | /etc/resolv.conf | 📝     | 📝    | ✔️      |
 | /etc/networks    | 📝     | 📝    | ✔️      |

> ❌ = Files can't be created, edited or removed                          <br>
> 📝 = Files can't be created and removed but file contents can be edited <br>
> ✔️ = Files can be created, edited and removed                            

# Usage:
```bash
immutablefs mode [mode]
```

Recommended:
```bash
immutablefs mode basic
``` 

# To unlock all system

```bash
immutablefs mode unlocked
```

# Dependencies:
 - Lua 5.3 or newer
