# Extract an IPA file on iOS

First, you need a jailbroken iPhone. Among the latest jailbreaking methods, Dopamine provides the newest approach, but there are some points to pay attention to.

1. The jailbreaking method provided by Dopamine is not a perfect jailbreak; it requires re-jailbreaking every time the device is restarted.
2. When using OpenSSH, the method is different from before. Previously, you would connect using `ssh root@<iPhone ip>` with the default password `alpine`. Now, the connection method is `ssh mobile@<iPhone ip>`, and the password is the one set during the jailbreaking process. If you want to use root privileges, use the `sudo su` command, and the password is still the one set during the jailbreak.
3. When using **Sileo** to download Frida, you first need to add the Frida repository. However, the downloaded Frida may cause the device to reboot during use. This issue can be resolved by downloading an older version from GitHub. I chose `frida_16.1.10_iphoneos-arm64.deb`. The downloaded package is sent to the iPhone via `scp file mobile@<iPhone ip>:/private/var/tmp` and then installed using `dpkg -i xxx.deb`.    

​    

Once Frida is ready, you can start dumping IPA files using the `frida-ios-dump` script. However, there are two points to note: in the `dump.py` file of `frida-ios-dump`, it still defaults to using the root username and the password `alpine` for login. You need to change `root` to `mobile`, and the password should be updated similarly as mentioned earlier—replace `alpine` with the password you set during jailbreaking.

​    

The final step is to obtain the **Bundle Identifier** of the corresponding app.

I used to check process names with the command `frida-ps -U`, which generally allows you to guess the process name based on the app's name. However, this is not a reliable method, as it can result in omissions. Therefore, it is recommended to use `ideviceinstaller -l -o list_user` to retrieve the correct Bundle Identifier. Finally, use the `frida-ios-dump` script to extract the corresponding IPA file.