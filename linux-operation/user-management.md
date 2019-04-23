# Add user - ROOT
```sh
adduser newuser

```
## Grant a User Sudo Privileges
```sh
groups newuser # check what groups now for this newuser
usermod -aG sudo newuser # grant newuser sudo privileges
```
## Specifying Explicit User Privileges in /etc/sudoers
As an alternative to putting your user in the sudo group, you can use the visudo command, which opens a configuration file called /etc/sudoers in the system's default editor, and explicitly specify privileges on a per-user basis.
<br>
Using visudo is the only recommended way to make changes to /etc/sudoers, because it locks the file against multiple simultaneous edits and performs a sanity check on its contents before overwriting the file. This helps to prevent a situation where you misconfigure sudo and are prevented from fixing the problem because you have lost sudo privileges.
<br>
If you are currently signed in as root, type:
```sh
visudo
```

```
Traditionally, visudo opened /etc/sudoers in the vi editor, which can be confusing for inexperienced users. By default on new Ubuntu installations, it should instead use nano, which provides a more familiar text editing experience. Use the arrow keys to move the cursor, and search for the line that looks like this:
                            /etc/sudoers
root    ALL=(ALL:ALL) ALL

                            /etc/sudoers
root    ALL=(ALL:ALL) ALL
newuser ALL=(ALL:ALL) ALL

You should add a new line like this for each user that should be given full sudo privileges. When you are finished, you can save and close the file by hitting Ctrl-X, followed by Y, and then Enter to confirm.

```

# Add user -no root
```sh
sudo adduser newuser
```


# Delete user
```sh
deluser newuser
```

## Delete the user's home directory when the user is deleted
```sh
deluser --remove-home newuser
```

If you had previously configured sudo privileges for the user you deleted, you may want to remove the relevant line again by typing:
```sh
visudo
```
