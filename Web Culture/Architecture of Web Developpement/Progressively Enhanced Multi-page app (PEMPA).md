### Document Request

**Document Request**: When the user requests the document for the first time, the same thing happens here as it does in the MPA example. However, a PEMPA will also load client-side JavaScript by including `<script>` tags which will be used for the enhancement capabilities.

![[Pasted image 20221017212205.png]]

### Client Side Navigation

**Client-side Navigation:** When the user clicks an anchor element with an `href` that is within our app, our client-side data fetching code prevents the default full-page refresh behavior and uses JavaScript to update the URL. Then the client routing logic determines what updates need to happen to the UI and manually performs those updates, including displaying any pending states (UI feedback) while the data fetching library makes a network request to a server endpoint. The server routing logic calls the data fetching code to retrieve data from the persistence code and sends that as a response which the client then uses to perform the final UI updates with its rendering logic.

### Redirect Mutation Request

**Mutation Requests:** When the user submits a form, our client-side data mutation logic prevents the default full-page refresh and post behavior and uses JavaScript to serialize the form and send the data to a server endpoint. The server routing logic then calls the data mutation function, which interacts with the persistence code to perform the mutation and responds with the updated data to the client. The client rendering logic will use that updated data to update the UI however is needed; in some cases the client-side routing logic will send the user to another place which triggers a similar flow to the client-side navigation flow.

![[Pasted image 20221017212447.png]]


### PEMPA Pros and cons

We definitely solved the problems with MPAs by bringing along client-side code and taking the UI Feedback responsibility onto ourselves. We have much more control and can give users a more custom app-like feel.

Unfortunately, to give the users the best experience they’re looking for, we have to be responsible for routing, data fetching, mutations, and rendering logic. There are a few problems with this:

1.  Prevent default - We don’t do as good a job as the browser does with routing and form submission. Keeping the data on the page up-to-date was never a concern before, but now it’s over half of our client-side code. Also, race conditions, form resubmissions, and error handling are great places for bugs to hide.
2.  Custom code - There’s a lot more code to manage that we didn’t have to write before. 
3.  Code duplication - There is a _lot_ of code duplication with regards to rendering logic. The client code needs to update the UI in the same way the backend code would render every possible state after a mutation or client transition. So the same UI that the backend has must be available in the frontend as well. And most of the time these are in completely different languages, which makes code sharing a non-starter. 
4.  Code organization - with PEMPAs this is very difficult. With no centralized place to store data or render UI, people were manually updating the DOM just about anywhere and it was very difficult to follow the code, which slowed down development.
5.  Server/Client indirection - There’s indirection between the API routes and the client-side data fetching and data mutation code that uses them. A change on one side of the network necessitates a change on the other side, and that indirection made it difficult to know we haven’t broken anything.

