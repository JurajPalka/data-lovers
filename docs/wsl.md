# WSL
Windows Subsystem for Linux is a compatibility layer for running Linux binary executables natively on Windows 10. 

# Installing specific version of python on WSL

## Installing python from source
If you compile Python from source, you must have the lzma-dev package installed, or it will not be built into python.

For ubuntu: `sudo apt-get install liblzma-dev` 

Instead of setting alternatives, you can set alias for your specific python version in `~/.bashrc`:
```
alias python='python3.9'
```

[Multiple python versions on Ubuntu][1]

[Using Python from WSL in VSCode][2]

[Encounter lsb_release issue?][3]

# SSH
To use SSH from windows
1. Install keychain `sudo apt-get install keychain`
2. Add the following code you the `~/.bashrc` file. Adjust path to your needs.

```
/usr/bin/keychain --nogui /mnt/c/users/john.smith/.ssh/john_github
source $HOME/.keychain/$HOSTNAME-sh
```

[More ways to enable SSH in WSL][4]

# EACCESS, cannot rename or move files
On WSL1 it is a known issue which has been fixed for WS2. To fix it, add to your VS Code settings the following setting:
`"remote.WSL.fileWatcher.polling": true`

[Developing in WSL][5]

[1]: https://hackersandslackers.com/multiple-versions-python-ubuntu/
[2]: https://docs.microsoft.com/en-us/windows/python/web-frameworks
[3]: https://stackoverflow.com/questions/44967202/pip-is-showing-error-lsb-release-a-returned-non-zero-exit-status-1
[4]: https://pscheit.medium.com/use-an-ssh-agent-in-wsl-with-your-ssh-setup-in-windows-10-41756755993e
[5]: https://code.visualstudio.com/docs/remote/wsl