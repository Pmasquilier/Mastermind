In the early days, this is the only architecture that worked at all on the web based on the capabilities of web browsers at the time.

With Multi-Page Apps, all of the code _we_ write lives on the server. The UI Feedback code on the client is handled by the user’s browser.
![[Pasted image 20221017193132.png]]


### MPA Architectural Behaviors

**Document Request:** When the user enters a URL in the address bar, the browser sends a request to our server. Our routing logic will call a function to fetch data which communicates with the persistence code to retrieve the data. This data then gets used by the rendering logic to determine the HTML which will be sent as a response to the client. All the while, the browser is giving the user feedback with some kind of pending state (normally in the favicon position).
![[Pasted image 20221017210608.png]]

### MPA Redirect Mutation Request

**Mutation Request:** When the user submits a form, the browser serializes the form into a request sent to our server. Our routing logic will call a function to mutate the data which communicates with the persistence code to make the database updates. Then it will respond with a redirect so the browser triggers a GET request to get fresh UI (which will trigger the same thing that happened when the user entered the URL to begin with). Again, the browser will give the user feedback with pending UI.
![[Pasted image 20221017210729.png]]

### MPA Cons

- Full-page refreshes (imagine a full-page refresh every time we liked a tweet…)
- UI Feedback control - It’s nice that the favicon turns into a spinner, but often a better UX is feedback that is visually closer to the UI the user interacted with.
