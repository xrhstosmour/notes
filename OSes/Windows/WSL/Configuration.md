#wsl-2 #configuration #restart-lxssmanager

To configure WSL 2, you'll need to edit the `.wslconfig` file located in your user's home directory (`C:\Users\<YourUsername>\.wslconfig`). If the file does not exist, you can create it. Here are the configurations you can apply:

### Set Memory Limit

To limit the amount of memory WSL 2 is allowed to use, you can specify the maximum memory. For example, to limit it to 8 GB, you can add the following line:

``` plaintext
[wsl2]
memory=8GB
```

### Set Processor Count

You can also specify the number of virtual processors used by the WSL 2 virtual machine. To set it to use 8 processors, add the following:

``` plaintext
processors=8
```

### Enable Localhost Forwarding

By default, ports bound to wildcard or localhost in the WSL 2 VM can be connected to from the host via `localhost:<port>`. To ensure this feature is enabled, you can explicitly set it:

``` plaintext
localhostForwarding=true
```

### Enable Nested Virtualization

If you're running a virtual machine inside WSL 2 and wish to use virtualization features inside this VM, you can enable nested virtualization:

``` plaintext
nestedVirtualization=true
```

### Conclusion

``` plaintext
[wsl2]

# Limits VM memory in WSL 2 to 8 GB.
memory=8GB

# Makes the WSL 2 VM use 8 virtual processors.
processors=8

# Boolean specifying if ports bound to wildcard or localhost in the WSL 2 VM should be connectable from the host via localhost:port.
localhostForwarding=true

# Enable nested virtualization
nestedVirtualization=true
```

## Applying the Configuration

After you have made the desired changes to the `.wslconfig` file, remember to restart the `LxssManager` service using PowerShell. Open PowerShell as an Administrator and run the following command:

``` powershell
Restart-Service LxssManager
```
