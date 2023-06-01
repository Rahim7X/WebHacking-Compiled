# Information Disclosure
Information disclosure is when attack can see any data from target assets
which is unintentional. The Impact is judge by the type of data which is disclosure
It is also reffered as Data Leakage.

### Such As 
- Data about other users
- Senstive commercial or business data
- Technical detials about the website and infrastructure

### Some Examples
- Revealing the name of hidden folders and files
- Can see backend sourcecode
- Database column names and table name in error messages
- Exposing high senstive information without need
- Hard-coding api keys

### Common sources of information disclosure

- Files for web crawlers
- Directory listings
- Developer comments 
- Error messages 
- Debugging data 
- User account pages 
- Backup files 
- Insecure configuration 
- Version control history (.git)

### Some Common Functions
- Leaking APIs
A leaking API is when a functioning-as-intended API, returns too much information.
- Dorking
Dorking for information is by far my personal favourite method.
Git Dork : postgress://username:password@subdomain
- Work Less
If you find any framework / endpoint low hanging bug then crrate a nuclei template
- Accidentally Public
Source Code, JS Files, API Keys, Crendetials
Meta Data Of Downloaded Image
- Directory Fuzzing (.json,.git)
- API ABuse
IDOR , SQLi

