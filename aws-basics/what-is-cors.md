# What is CORS (Cross-Origin Resource Sharing)?

## Memory Hook
- “Same origin = safe. Cross origin? Ask for permission.”
- “CORS is a browser-level security contract — not a firewall rule.”

## Why Was CORS Invented?
- CORS exists because browsers enforce the Same-Origin Policy (SOP) by default:
- Same-Origin Policy says:
- “A web page can only make requests to the same origin it came from.”

## What is an origin?
- Origin = Scheme + Hostname + Port
- Example:
- https://api.example.com ≠ http://api.example.com
- https://example.com ≠ https://sub.example.com

- SOP protects users from malicious JavaScript on one website stealing data from another (e.g., bank.com).

## What’s the Problem?
- Frontend apps (React, Angular, etc.) often call APIs hosted on other domains — a different origin.
- For example:
- Your app is served from: https://myfrontend.com
- Your API is hosted at: https://api.mycompany.com
- Browser will block this request due to cross-origin restriction, even though you own both.

## Why Not Just Use IP/Hostname-Based Blocking?
- Because those are server-side filtering tools:
- IP filters = Layer 3/4
- DNS/hostname rules = routing
- Headers = not enforced by browsers

- CORS is not about blocking on the server — it’s about the browser deciding what’s allowed to happen on behalf of the user.
- CORS is enforced by browsers, not by servers or AWS.

## How Does CORS Work?
- Step-by-Step
- Let’s say your app running on https://myapp.com wants to GET an image from https://cdn.example.com.

- 1. Browser makes a preflight OPTIONS request (if needed)
```
	OPTIONS /image.png
	Origin: https://myapp.com
	Access-Control-Request-Method: GET
```
- 2. Server responds with CORS headers
```
	Access-Control-Allow-Origin: https://myapp.com
	Access-Control-Allow-Methods: GET
```
- 3. Browser evaluates:
- “Is my origin allowed?” ✅
- “Is my method allowed?” ✅
- Then it sends the actual GET request.

## Simple vs Preflight Requests
- Type	| When it happens
- Simple request	| GET/HEAD/POST with standard headers
- Preflight request	| Any other method or custom headers

### Preflight uses OPTIONS method

