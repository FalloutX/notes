# Progressive Web App Components
> Last Updated 19th Jan 2017.

## Client-Side Storage

<br/>
#### Cookies

| Compatibility | Everywhere!                              |
| ------------- | ---------------------------------------- |
| Size          | Max 4KB                                  |
| Data Type     | string                                   |
| Pros          | Simple, Configurable, Compatible         |
| Cons          | Less Secure, Limiting, Attaches to every request, easily deletable. |


#### HTML Web Storage (localStorage & sessionStorage)

| Compatibility | Everywhere!                          |
| ------------- | ------------------------------------ |
| Size          | 2.5 - 5 MB                           |
| Data Type     | string                               |
| Pros          | Simple, Not Transimitted, Compatible |
| Cons          | Unstructured data, slow access.      |


#### Web SQL

| Compatibility | Chrome, Safari, Opera, Strong Mobile Support |
| ------------- | ---------------------------------------- |
| Size          | 2.5 - 5 MB                               |
| Data Type     | string                                   |
| Pros          | Asynchronous, great search speed.        |
| Cons          | Deprecated, Steep learning curve, Schema pre-defined. |


#### Indexed DB

| Compatibility | Modern Browsers, lacks Mobile Support    |
| ------------- | ---------------------------------------- |
| Size          | 10 - 20% of the available space(based on Browser!) |
| Data Type     | JSObject                                 |
| Pros          | Asynchronous, Large Dataset              |
| Cons          | Steep learning curve, Complicated while implementing. |

## Service Workers

#### Basics

- Service Worker scripts run independently from our app code.
- Separate Thread.
- Intercept Network Requests.
- Functional Events (fetch, push, sync)
- Available in Chrome, Firefox & Opera(not all updates).
- Needs to be served with HTTPS.
- No Access to the DOM, Runs on its own Global script context.
- Not tied to any page.
- Event-Driven.
