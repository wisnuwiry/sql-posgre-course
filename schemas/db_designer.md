```
Table users {
  id SERIAL [increment, pk]
  username VARCHAR(30)
  bio VARCHAR(400)
  avatar VARCHAR(200)
  phone VARCHAR(25)
  email VARCHAR(40)
  password VARCHAR(50)
  status VARCHAR(15)
  created_at TIMESTAMP
  updated_at TIMESTAMP
}

Table posts {
  id SERIAL [increment, pk]
  url VARCHAR(200)
  created_at TIMESTAMP
  updated_at TIMESTAMP
  caption VARCHAR(240)
  lat REAL
  lng REAL
}

<!-- Comment -->
Table comments {
  id SERIAL [increment, pk]
  user_id INTEGER [ref: > users.id]
  post_id INTEGER [ref: > posts.id] 
  contents VARCHAR(240)
  created_at TIMESTAMP
  updated_at TIMESTAMP
}

<!-- Likes -->
Table likes {
  id SERIAL [increment, pk]
  user_id INTEGER [ref: > users.id]
  post_id INTEGER [ref: > posts.id] 
}

Table reactions {
  id SERIAL [increment, pk]
  user_id INTEGER [ref: > users.id]
  post_id INTEGER [ref: > posts.id] 
  type VARCHAR(50)
}

<!-- Mention -->
Table photo_tags {
  id SERIAL [pk, increment]
  post_id INTEGER [ref: > posts.id]
  user_id INTEGER [ref: > users.id]
  x INTEGER
  y INTEGER
  created_at TIMESTAMP
}

Table caption_tags {
  id SERIAL [pk, increment]
  post_id INTEGER [ref: > posts.id]
  user_id INTEGER [ref: > users.id]
  created_at TIMESTAMP
}

<!-- Hashtags -->
Table hashtags {
  id SERIAL [pk, increment]
  title VARCHAR(20)
  created_at TIMESTAMP
}

Table hashtags_posts {
  id SERIAL [pk, increment]
  hashtag_id INTEGER [ref: > hashtags.id]
  post_id INTEGER [ref: > posts.id]
}
```