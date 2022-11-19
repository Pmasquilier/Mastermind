If we could somehow merge SPAs and MPAs into a single architecture to get the best of both, then hopefully we’ll have something that is both simple and more capable. That’s what Progressively Enhanced Single Page Apps are.

## PESPA Architectural Behaviors

### Document Request

Document requests with PESPAs are effectively identical to PEMPAs. The initial HTML needed for the app is sent straight from the server and JavaScript is also loaded to enhance the experience for user interactions.

![[Pasted image 20221017214101.png]]

### Client-Side Navigation

**Client-side Navigation:** When the user clicks a link, we’ll prevent the default behavior. Our router will determine the data and UI needed for the new route and trigger data fetching for whatever data the next route needs and render the UI that’s rendered for that route.

![[Pasted image 20221017214132.png]]


### Redirect Mutation Request

**Mutation Requests:** When the user submits a form, we’ll prevent the default behavior. Our mutation code serializes the form and sends it as a request to the route associated to the `action` of the form (which defaults to the current URL). The routing logic on the backend calls the action code which communicates with the persistence code to perform the update and sends back a successful response (for example: a tweet like) or redirect (for example: creating a new GitHub repo). If it’s a redirect, the router loads code/data/assets for that route (in parallel) and then triggers the rendering logic. If it’s not a redirect, the router revalidates the data for the current UI and triggers the rendering logic to update the UI. Interestingly though, regardless of whether it’s an inline mutation or a redirect, the router is involved, giving us the same mental model for both types of mutations.
![[Pasted image 20221017214233.png]]

### What distinguishes a PESPA:

-   Functional is the baseline - JS used to enhance not enable
-   Lazy loading + intelligent pre-fetching (more than just JS code)
-   Pushes code to the server
-   No manual duplication of UI code (as in PEMPAs)
-   Transparent browser emulation (#useThePlatform)

## The new wave of Javascript web frameworks

Inspired by PHP, Next stepped up to streamline the process of creating static pages pushed to a CDN. It also smoothed over the hairy parts of using SSR in React apps.

It came with some much-wanted opinions on structuring an app, using file-based routing. And a bunch of other nice features.

Since then a wave of other “meta” frameworks were created. For Vue, we have a similar framework in Nuxt. Svelte’s Sveltekit, and the up and coming SolidStart.

These are server-first, designed to integrate all pieces and ergonomics of a web framework. Not only the interactive element that has been in the spotlight for a long time.
