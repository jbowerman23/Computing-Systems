# Application Layer and DNS
---

## [Slides](https://redhawks-my.sharepoint.com/:p:/r/personal/bowermanjess_seattleu_edu/_layouts/15/Doc.aspx?sourcedoc=%7B689DDC5D-DB38-4626-A6F5-5C59AA594345%7D&file=9-Transport-Layer.pptx&action=edit&mobileredirect=true)
---

## What does the application layer do?
- Fundamental responsibility is to provide various networking services to users
  - Domain Name System (DNS)
  - File Transfer Protocol (FTP)
  - Simple Mail Transfer Protocol (SMTP)
  - Hypertext Transfer Protocol (HTTP)

---

## Domain Name System (DNS)
- Support service for several other protocols
- Names are easier for humans to remember than IP addresses
- Names help with portability even when IP address changes
- Internally we need some way to translate human readable name to IP address…
- …DNS resolves human-readable names to IP addresses
- Like the hierarchical IP address space
- DNS supports hierarchical, domain-based naming system

![image](https://user-images.githubusercontent.com/102563482/171454392-b0146dcd-03e3-4cbf-9458-46b91653b566.png)

- DNS maintains and uses name servers
- Every name server contains name to IP address mapping to a portion of the namespace called zones

### How are names mapped to IP addresses?
- The formal name for finding IP address for given hostname -> resolution
  - Computer request local name server to resolve (ask what IP address for name)
  - Local name server is now tasked with finding out what name an IP address maps to
  - First, local name server contacts root name server (top-level)
  - Root server tells local name server the details of the name server for lower zone
  - Local name server contacts this new name server which may have the answer…
  - …Or may know info about another name server that is relevant in zone below it

  - It will continue down the zones until a particular name server can answer

![image](https://user-images.githubusercontent.com/102563482/171454895-0fabd568-7ed3-4e23-83eb-3180dcef0103.png)

---

## World Wide Web (www)
- Let’s delve into the World Wide Web & protocol it uses
- From user perspective, Web is vast collection of pages
- Pages named with Uniform Resource Locators (URLs)
  - Example: http://www.phdcomics.com/comics.php

- View of page on browser is result of conversation between browser (client) and web server (server)
  - Communication language: Hypertext Transfer Protocol (HTTP)

---

## Hypertext Transfer Protocol (https)
### Request message
  - Initial request line: method + local path + HTTP version #
  - Request header: information about request
    - Acceptable content types in response
    - Acceptable human language in response
    - Email address of requestor

  - Blank line
  - Optional message body
    - Data entered by user that needs to be sent to the server
    - Contents of a file being uploaded

- HTTP has several request methods
<img width="376" alt="image" src="https://user-images.githubusercontent.com/102563482/171455481-8d95de16-fced-4493-97c4-25ea32eb0381.png">

### Response message
- Initial response line: HTTP version + status + reason
- Response header: information about response
  - Timestamp
  - Content type
  - Content length

- Blank line
- Optional message body
  - File content
  - Output of some query that was submitted

- Status field in initial response line is response code to tell client what happened to its request

<img width="700" alt="image" src="https://user-images.githubusercontent.com/102563482/171455831-4ef607ea-9135-46ee-9672-6f7f18d961aa.png">










