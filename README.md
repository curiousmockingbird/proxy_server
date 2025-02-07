# Vue.js Pagination with EveryAction API

**Paginated** fetching of event data from the EveryAction API. It consists of:

1. **Proxy Server** (Serverless function / Node endpoint)  
2. **Vue.js Component** that handles **state** and **UI** for displaying paginated events.

---

## Overview

- **Goal:** Show events in smaller, more manageable batches, giving the user the option to load more if needed.  
- **Technologies:**
  - **Vue.js** for the front-end UI.
  - **Axios** for HTTP requests.
  - **Node.js / Serverless Function** as a proxy to the EveryAction API.
  - **EveryAction API** for the event data source.

---

## Features

1. **Server-Side Pagination Parameters**
   - The serverless (proxy) endpoint accepts a `page` query parameter and calculates `skip = page * pageSize`.
   - Queries EveryAction with `&$top=pageSize&$skip=skip` to fetch the correct slice of events.
   - Returns a JSON response containing:
     - `items`: Array of events for the current page.
     - `hasMore` or `nextPageLink` (optional): Indicates if additional pages remain.

2. **Vue.js Pagination State**
   - Maintains `currentPage`, `hasMore`, `loading`, and an array of `events`.
   - Calls the proxy endpoint with `?page=${currentPage}` to fetch additional pages.
   - Shows a “Load More” button if more events are available.

3. **Responsive Event List**
   - Displays a small batch (e.g., 10 events) initially, then appends more on demand.
   - Improves performance, especially if the total number of events is large.

---