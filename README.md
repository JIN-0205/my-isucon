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


### Put a index
- Enabled MySQL slow query log
- Identified full table scan on `comments`
- Added indexes:
  - `comments(post_id, created_at)`
  - `comments(post_id)`
- Result:
```json
{"pass":true,"score":10577,"success":9706,"fail":0,"messages":[]}
```

### Set Limit posts query
- add `LIMIT 50` to `posts`
- Result:
```json
{"pass":true,"score":12280,"success":11189,"fail":0,"messages":[]}
```

### Add indexes to posts.created_at and comments.user_id
- Identified slow queries from MySQL slow query log:
  - Posts list query with `ORDER BY created_at DESC LIMIT 50` causing large `Rows_examined`
  - User comment count query with `SELECT COUNT(*) FROM comments WHERE user_id = ?` causing full table scan
- Added indexes:
  - `posts(created_at)`
  - `comments(user_id)`
- Result:
```json
{"pass":true,"score":14091,"success":12766,"fail":0,"messages":[]}