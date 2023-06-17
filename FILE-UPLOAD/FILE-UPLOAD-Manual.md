# Upload Vulnerbilities 
- Bypassing Client Side Filters
- BruteForcing Extensions
- Content Type And Magic Bytes
- File Upload Using Python
- Content Type Python 
- Path Traversal
- rconfig 3.9.6 FIle Upload RCE via Python

## File Upload Extension
```bash
Try these file-uploading extensions accordingly.

ASP Applications:

.asa -> potential remote code execution

.asax -> potential remote code execution

.asp -> potential remote code execution

.aspx -> potential remote code execution

Java Applications: 

.jsp -> potential remote code execution

.jspx -> potential remote code execution

Perl Applications: 

.pl -> potential remote code execution

Python Applications: 

.py -> potential remote code execution

Ruby Applications:

.rb -> potential remote code execution

Other files that should be restricted for most applications: 

.bat
.cgi
.exe
.htm -> potential XSS
.html -> potential XSS
.jar
.rar
.shtml
.svg -> potential XSS
.swf -> potential XSS
.tar
.zip
.cer -> potential XSS
.hxt -> potential XSS
.stm -> potential XSS
```
