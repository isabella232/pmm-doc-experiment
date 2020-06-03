# VirtualBox Using the Command Line

Instead of using the {{ virtualbox }} GUI, you can do everything on the command
line. Use the `VBoxManage` command to import, configure, and start the
appliance.

The following script imports the {{ pmm_server }} appliance from
{{ pmm_server_1_6_0_ova }} and configures it to bridge the en0 adapter from the
host.  Then the script routes console output from the appliance to
{{ tmp_pmm_server_console_log }}.  This is done because the script then starts the
appliance in headless (without the console) mode.

To get the IP address for accessing PMM, the script waits for 1 minute until the
appliance boots up and returns the lines with the IP address from the log file.

```
# Import image
VBoxManage import pmm-server-|VERSION NUMBER|.ova

# Modify NIC settings if needed
VBoxManage list bridgedifs
VBoxManage modifyvm 'PMM Server [VERSION NUMBER]' --nic1 bridged --bridgeadapter1 'en0: Wi-Fi (AirPort)'

# Log console output into file
VBoxManage modifyvm 'PMM Server [VERSION NUMBER]' --uart1 0x3F8 4 --uartmode1 file /tmp/pmm-server-console.log

# Start instance
VBoxManage startvm --type headless 'PMM Server [VERSION NUMBER]'

# Wait for 1 minute and get IP address from the log
sleep 60
grep cloud-init /tmp/pmm-server-console.log
```

In this script, `[VERSION NUMBER]` is the placeholder of the version of
{{ pmm_server }} that you are installing. By convention **OVA** files start with
*pmm-server-* followed by the full version number such as 2.6.0.

To use this script, make sure to replace this placeholder with the the name of
the image that you have downloaded from the [Download Percona Monitoring and
Management](https://www.percona.com/downloads/pmm) site. This script also assumes that you have changed the working
directory (using the {{ cd }} command, for example) to the directory which contains
the downloaded image file.

### Downloading the latest development version
