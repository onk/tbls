# testdb

## Description

Sample database document.

## Labels

`sample` `tbls`

## Tables

| Name | Columns | Comment | Type | Labels |
| ---- | ------- | ------- | ---- | ------ |
| [CamelizeTable](CamelizeTable.md) | 2 |  | BASE TABLE |  |
| [comment_stars](comment_stars.md) | 6 |  | BASE TABLE |  |
| [comments](comments.md) | 7 | Comments<br>Multi-line<br>table<br>comment | BASE TABLE |  |
| [hyphen-table](hyphen-table.md) | 3 |  | BASE TABLE |  |
| [logs](logs.md) | 7 | Auditログ | BASE TABLE |  |
| [post_comments](post_comments.md) | 7 | post and comments View table | VIEW |  |
| [posts](posts.md) | 7 | Posts table | BASE TABLE | `green` `red` `blue` |
| [user_options](user_options.md) | 4 | User options table | BASE TABLE |  |
| [users](users.md) | 6 | Users table | BASE TABLE |  |

## Stored procedures and functions

| Name | ReturnType | Arguments | Type |
| ---- | ------- | ------- | ---- |
| CustomerLevel | varchar | credit decimal | FUNCTION |
| GetAllComments |  |  | PROCEDURE |

## Relations

```mermaid
erDiagram

"comment_stars" }o--|| "users" : "FOREIGN KEY (comment_user_id) REFERENCES users (id)"
"comment_stars" }o--|| "comments" : "FOREIGN KEY (comment_post_id, comment_user_id) REFERENCES comments (post_id, user_id)"
"comments" }o--|| "posts" : "FOREIGN KEY (post_id) REFERENCES posts (id)"
"comments" }o--|| "users" : "FOREIGN KEY (user_id) REFERENCES users (id)"
"posts" }o--|| "users" : "FOREIGN KEY (user_id) REFERENCES users (id)"
"user_options" |o--|| "users" : "FOREIGN KEY (user_id) REFERENCES users (id)"
"logs" }o--|| "users" : "logs-&gt;users"
"logs" }o--o| "posts" : "Additional Relation"
"logs" }o--o| "comments" : "Additional Relation"
"logs" }o--o| "comment_stars" : "Additional Relation"

"CamelizeTable" {
  bigint id PK
  datetime created
}
"comment_stars" {
  bigint id PK
  int user_id
  bigint comment_post_id FK
  int comment_user_id FK
  timestamp created
  timestamp updated
}
"comments" {
  bigint id PK
  bigint post_id FK
  int user_id FK
  text comment
  bigint post_id_desc
  datetime created
  datetime updated
}
"hyphen-table" {
  bigint id PK
  text hyphen-column
  datetime created
}
"logs" {
  bigint id PK
  int user_id
  bigint post_id
  bigint comment_id
  bigint comment_star_id
  text payload
  datetime created
}
"post_comments" {
  bigint id
  varchar_255_ title
  varchar_50_ post_user
  text comment
  varchar_50_ comment_user
  datetime created
  datetime updated
}
"posts" {
  bigint id PK
  int user_id FK
  varchar_255_ title
  text body
  enum__public___private___draft__ post_type
  datetime created
  datetime updated
}
"user_options" {
  int user_id PK
  tinyint_1_ show_email
  timestamp created
  timestamp updated
}
"users" {
  int id PK
  varchar_50_ username
  varchar_50_ password
  varchar_355_ email
  timestamp created
  timestamp updated
}
```

---

> Generated by [tbls](https://github.com/k1LoW/tbls)
