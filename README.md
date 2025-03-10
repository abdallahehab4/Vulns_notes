# Vulns_notes
## Manually Walking Through the Target  

Before starting recon, manually explore the application to understand its features.  

### Steps:  
- Browse all pages, click every link, and test uncommon functionalities.  
  - Example: On Facebook, create an event, play a game, or use payments.  
- Sign up at **all privilege levels** to reveal hidden features.  
  - Example: In Slack, create owners, admins, and members, and test different channels.  

### Why?  
- Maps the **attack surface** (entry points for attackers).  
- Identifies **data entry points** and user interactions.  
- Prepares for deeper reconnaissance (tech & structure analysis).  

Once familiar with the app, move on to detailed recon.  

## Google Dorking  

Google dorking is an advanced search technique that helps hackers and security researchers discover valuable information, such as **hidden admin portals, leaked files, and vulnerable endpoints**.  

### Key Google Dorking Operators  

 ### `site`
 Tells Google to show you results from a certain site only. This will help 
you quickly find the most reputable source on the topic that you are 
researching. For example, if you wanted to search for the syntax of 
Python’s print() function, you could limit your results to the official 
Python documentation with this search: print site:python.org.
 ### `inurl`
 Searches for pages with a URL that match the search string. It’s a pow
erful way to search for vulnerable pages on a particular website. Let’s 
say you’ve read a blog post about how the existence of a page called  
/course/jumpto.php on a website could indicate that it’s vulnerable to remote 
code execution. You can check if the vulnerability exists on your target by 
searching inurl:"/course/jumpto.php" site:example.com.
 ### `intitle`
 Finds specific strings in a page’s title. This is useful because it allows you 
to find pages that contain a particular type of content. For example, 
file-listing pages on web servers often have index of in their titles. 
You can use this query to search for directory pages on a website: 
intitle:"index of" site:example.com.
 ### `link`
 Searches for web pages that contain links to a specified URL. You can 
use this to find documentation about obscure technologies or vulner
abilities. For example, let’s say you’re researching the uncommon regu
lar expression denial-of-service (ReDoS) vulnerability. You’ll easily pull 
up its definition online but might have a hard time finding examples. 
The link operator can discover pages that reference the vulnerability’s 
Wikipedia page to locate discussions of the same topic: link:"https://
 en.wikipedia.org/wiki/ReDoS".
 ### `filetype`
 Searches for pages with a specific file extension. This is an incredible 
tool for hacking; hackers often use it to locate files on their target sites 
that might be sensitive, such as log and password files. For example, this 
query searches for log files, which often have the .log file extension, on 
the target site: filetype:log site:example.com.
 ### `Wildcard (*)`
 You can use the wildcard operator (*) within searches to mean any char
acter or series of characters. For example, the following query will return 
any string that starts with how to hack and ends with using Google. It will 
63
 Web Hacking Reconnaissance   
match with strings like how to hack websites using Google, how to hack appli
cations using Google, and so on: "how to hack * using Google".
 ### `Quotes (" ")`
 Adding quotation marks around your search terms forces an exact match. 
For example, this query will search for pages that contain the phrase how 
to hack: "how to hack". And this query will search for pages with the terms 
how, to, and hack, although not necessarily together: how to hack.
 ### `Or (|)`
 The or operator is denoted with the pipe character (|) and can be used 
to search for one search term or the other, or both at the same time. 
The pipe character must be surrounded by spaces. For example, this 
query will search for how to hack on either Reddit or Stack Overflow: 
"how to hack" site:(reddit.com | stackoverflow.com). And this query will 
search for web pages that mention either SQL Injection or SQLi: (SQL 
Injection | SQLi). SQLi is an acronym often used to refer to SQL injec
tion attacks, which we’ll talk about in Chapter 11.
 ### `Minus (-)`
 The minus operator (-) excludes certain search results. For example, 
let’s say you’re interested in learning about websites that discuss hacking, 
but not those that discuss hacking PHP. This query will search for pages 
that contain how to hack websites but not php: "how to hack websites" -php.

### For new quires `https://www.exploit-db.com/google-hacking-database`

## WHOIS and Reverse WHOIS  

When companies or individuals register a domain name, they must provide identifying information, such as their **mailing address, phone number, and email**, to a domain registrar. This information can be queried using the `whois` command to retrieve the registrant and owner details of a domain.  

### WHOIS Lookup  
The `whois` command can reveal details such as:  
- The **owner's name or company**  
- **Email address and contact information**  
- **Domain registration and expiration dates**  
- **Associated name servers**
- **https://viewdns.info/reversewhois**

## Reverse IP Lookup Guide

### What is an IP Address?
An IP address is a unique identifier assigned to each device connected to a network using the Internet Protocol (IP). It can be either IPv4 (e.g., `192.168.1.1`) or IPv6 (e.g., `2001:db8::ff00:42:8329`).

---

### Finding the IP Address of a Domain
You can discover the IP address of a domain using the `nslookup` command:

```bash
$ nslookup facebook.com
Server: 192.168.0.1
Address: 192.168.0.1#53
Non-authoritative answer:
Name: facebook.com
Address: 157.240.2.35
```

---

### Reverse IP Lookup
Once you have an IP address, you can perform a **Reverse IP Lookup** to find other domains hosted on the same server.

### 1. Using ViewDNS.info
- Visit: [ViewDNS.info Reverse IP Lookup](https://viewdns.info/reverseip/)
- Enter the target IP (e.g., `157.240.2.35`).
- Click **Submit** to see a list of domains sharing the same server.

### 2. Using Shodan
Shodan is a powerful search engine for internet-connected devices.

#### **Using Shodan Web Interface:**
- Go to: [Shodan.io](https://www.shodan.io/)
- Log in or create an account.
- Search for the IP address (e.g., `157.240.2.35`).
- View associated domains, open ports, and services.

#### **Using Shodan CLI:**
```bash
shodan host 157.240.2.35
```

### 3. Using SecurityTrails
- Visit: [SecurityTrails](https://securitytrails.com/)
- Sign up for a free account.
- Enter the IP address and review related domains.

### 4. Using Bing Search
You can also use Bing to find related domains by searching:
```
ip:157.240.2.35
```

---

## Using WHOIS to Identify IP Ranges
Use the `whois` command to determine if the target has a dedicated IP range:

```bash
$ whois 157.240.2.35
```
Example output:
```
NetRange: 157.240.0.0 - 157.240.255.255
```
This indicates that all IPs within this range belong to the same organization.

---

## Why is Reverse IP Lookup Useful for Pentesting?
- **Discover additional assets** related to a target.
- **Identify unsecured servers** on the same hosting.
- **Map an organization's infrastructure** for reconnaissance.
- **Find outdated web applications** that share the same IP.

## IP Discovery and ASN Analysis

### 1. Find the IP Address of a Domain
To find the IP address of a target domain, use the `nslookup` command:

```bash
$ nslookup examplecorp.com
```
**Example Output:**
```
Server:  192.168.1.1
Address: 192.168.1.1#53

Non-authoritative answer:
Name:    examplecorp.com
Address: 203.0.113.50
```

---

### 2. Perform a Reverse IP Lookup
To find other domains hosted on the same server, use tools like:
- [ViewDNS.info](https://viewdns.info/reverseip/)
- Shodan
- SecurityTrails

### Using Shodan:
```bash
$ shodan host 203.0.113.50
```
**Example Output:**
```
203.0.113.50
Domains: 
- examplecorp.com
- examplecorp.net
- test.examplecorp.com
```

---

### 3. Get ASN Information of an IP
To identify the ASN (Autonomous System Number) of an IP, use the `whois` command:

```bash
$ whois 203.0.113.50
```
**Example Output:**
```
NetRange:       203.0.113.0 - 203.0.113.255
OriginAS:       AS65001
Organization:   Example Corp, Inc.
```

---

### 4. Find the Entire IP Range of the Target
Once you have the ASN, check for all associated IP ranges using [BGPView.io](https://bgpview.io/):
1. Go to [BGPView.io](https://bgpview.io/)
2. Search for ASN `AS65001`
3. Example IP ranges found:
   ```
   203.0.113.0/24
   198.51.100.0/24
   ```

---

## 5. Verify That Another IP Belongs to the Same ASN
To confirm that an additional IP belongs to the same ASN:

```bash
$ whois 198.51.100.25
```
**Example Output:**
```
NetRange:       198.51.100.0 - 198.51.100.255
OriginAS:       AS65001
Organization:   Example Corp, Inc.
```

---

### Summary of Steps

| **Step** | **Command / Tool** | **Purpose** |
|------------|----------------|----------------|
| 1. Find IP of a domain | `nslookup examplecorp.com` | Get the IP address of the target domain |
| 2. Reverse IP Lookup | `shodan host 203.0.113.50` | Discover other domains on the same server |
| 3. Extract ASN Info | `whois 203.0.113.50` | Find the ASN associated with the IP |
| 4. Find All IPs Owned by ASN | [BGPView.io](https://bgpview.io/) | Get all IP ranges linked to the ASN |
| 5. Verify Ownership of Another IP | `whois 198.51.100.25` | Confirm if another IP belongs to the same ASN |

By following these steps, you can map the target’s infrastructure, identify additional assets, and expand the attack surface for penetration testing and bug bounty hunting.




