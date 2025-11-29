| Code | Category | Meaning | When It's Used |
| --- | --- | --- | --- |
| 200 OK | Success | Request succeeded | Standard successful GET/POST/PUT/PATCH |
| 201 Created | Success | Resource was created | POST creating a new item/user |
| 204 No Content | Success | Operation succeeded, no body returned | DELETE or successful update without response |
| 301 Moved Permanently | Redirect | Resource moved to a new URL | Permanent redirect |
| 302 Found | Redirect | Temporary redirect | Login redirects, temporary moves |
| 304 Not Modified | Redirect | Cached version is still valid | Browser caching |
| 400 Bad Request | Client Error | Invalid request format | Missing fields, wrong JSON |
| 401 Unauthorized | Client Error | Auth required or failed | Missing/invalid token |
| 403 Forbidden | Client Error | Client authenticated but not allowed | No permissions |
| 404 Not Found | Client Error | Resource does not exist | Wrong ID, wrong URL |
| 409 Conflict | Client Error | Conflict with current state | Duplicate entries, version conflicts |
| 429 Too Many Requests | Client Error | Rate limiting | API throttling |
| 500 Internal Server Error | Server Error | Unexpected server failure | Unhandled exception |
| 502 Bad Gateway | Server Error | Upstream server error | Proxy/load balancer issue |
| 503 Service Unavailable | Server Error | Server down or overloaded | Maintenance, outages |
| 504 Gateway Timeout | Server Error | Upstream server didn't respond in time | Slow microservice |



