--- 
## What is REST API?

## 6 Principles

#### Uniform interface
- Announce **available actions** + **resources**
- **Identification of resources**: 
	- Use standard URI to uniquely identify resources
- **Manipulation of resources through these representations** 
	- You use the HTTP standard to describe communication. So for example GET means that you want to retrieve data about the URI-identified resource. You can describe an operation with an HTTP method and a URI.
	- JSON or XML for response
- **Self-descriptive messages** 
	- Each resource representation should carry sufficient information to describe how to process the message. It should also provide the client the **semantics** to find the data
	- e.g.  Status Code, MIME types, (standard) [RDF vocabs](https://developer.mozilla.org/en-US/docs/Glossary/RDF) 
		- .jpeg, .pdf, application/json
- **Hypermedia as the engine of application state** (a.k.a. HATEOAS) 
	- Transition by hyperlinks and possibly [URI templates](https://en.wikipedia.org/wiki/URI_Template) 
		- By including links in returned representations, the server can remove the burden from the user-agent of **determining what actions can be taken based on the current application state**
		- Clients can now use these URLs from the response and be sure that these URLs are the latest versions.
	- The system has NO knowledge of user agent's state, becomes loosely coupled as the URLs do not require hard-coding. 
	- Simple mechanism, declarative. just follow the link for the next step

#### Client-server
- Separation of concern between server and client
#### Stateless
- Request are independent
- No state is preserved. Server always give up-to-date information? 
#### Cacheable
#### Layered system
#### Code on demand (optional)
https://www.techtarget.com/searchapparchitecture/tip/The-5-essential-HTTP-methods-in-RESTful-API-development
http://rest.elkstein.org/2008/02/rest-design-guidelines.html
https://www.w3.org/Provider/Style/URI



- Use Logical URLs instead of physical URI
FALSE: A paging technique should be used if the output data is small
- should be large
FALSE: Actual URLs must always be used in REST response
-  responses do not necessarily need to include actual URLs. They can include resource identifiers or other data
TRUE: GET requests must be read-only
TRUE: output format can be changed
FALSE: PUT request must be read-only

https://www.veryshares.com/rest.html

#### Good URIs design
---
1,3,4,5
- URIs should never be changed
- Case-sensitive
- As s
TRUE: URIs should never be changed
FALSE : Use HTTPP verbs
TRUE: should be case-sensrtive
TRUE: Short
ture: Redirection must be used if a change in URI is required

#### server repsone format
---
**CSV, XML, and JSON**