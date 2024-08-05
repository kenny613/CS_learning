## Render Lifecycle 
1. `DOMContentLoaded`: HTML document has been fully loaded and parsed, without waiting for stylesheets, images, and subframes to finish loading
2. `load`: All dependent resources such as stylesheets and images, has loaded.
3. `beforeunload`: 

## Network lifecycle after HTTP request
https://dev.to/ashevelyov/the-step-by-step-journey-of-a-network-request-1d10
#### DNS Request
#### TCP 3 way handshake
- After **IP address** is found
- ![[Pasted image 20240803234445.png|500]]
#### Sending HTTP request
![[Pasted image 20240803234514.png|500]]

# Critical rendering path


# Q&A
---
#### When is DOMContentLoaded?
- The **`DOMContentLoaded`** event fires when the HTML document has been completely parsed, and all deferred scripts ([`<script defer src="…">`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/script#defer) and [`<script type="module">`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/script#module)) have downloaded and executed. It doesn't wait for other things like images, subframes, and async scripts to finish loading.
#### NEw HTML5 tags
https://www.tutorialspoint.com/html5/html5_new_tags.htm