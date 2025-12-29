# my-isucon

## ISUCON tuning log

### Initial score


```json
{"pass":true,"score":73,"success":493,"fail":23,
 "messages":[
   "リクエストがタイムアウトしました (GET /)",
   "リクエストがタイムアウトしました (GET /logout)",
   "リクエストがタイムアウトしました (POST /login)",
   "リクエストがタイムアウトしました (POST /register)"
 ]}
 ```


### 2025-12-29
- Enabled MySQL slow query log
- Identified full table scan on `comments`
- Added indexes:
  - `comments(post_id, created_at)`
  - `comments(post_id)`
- Result:
```json
{"pass":true,"score":10577,"success":9706,"fail":0,"messages":[]}
```
