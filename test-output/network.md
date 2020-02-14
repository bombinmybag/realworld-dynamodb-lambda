```
DELETE /__TESTUTILS__/purge
```
```
200 OK

"Purged all data!"
```
# Article
```
POST /users

{
  "user": {
    "email": "author-m61aty@email.com",
    "username": "author-m61aty",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "author-m61aty@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvci1tNjFhdHkiLCJpYXQiOjE1ODE3MjA0MjYsImV4cCI6MTU4MTg5MzIyNn0.6zizlUrU9tIctAoz1xB3iPscwWe8lAIiq4uexqK3KqY",
    "username": "author-m61aty",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "authoress-8ayl95@email.com",
    "username": "authoress-8ayl95",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "authoress-8ayl95@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvcmVzcy04YXlsOTUiLCJpYXQiOjE1ODE3MjA0MjYsImV4cCI6MTU4MTg5MzIyNn0.9fkZUFxtFUpAydunzYrLhKmT4L3YZLAXi7gE0dhVcwk",
    "username": "authoress-8ayl95",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "non-author-1z1nzc@email.com",
    "username": "non-author-1z1nzc",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "non-author-1z1nzc@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6Im5vbi1hdXRob3ItMXoxbnpjIiwiaWF0IjoxNTgxNzIwNDI2LCJleHAiOjE1ODE4OTMyMjZ9.TITm1gDotXMc1QxPg71uCI9pAzAjg9E-Gw335yBgNkM",
    "username": "non-author-1z1nzc",
    "bio": "",
    "image": ""
  }
}
```
## Create
### should create article
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body"
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-2m3fsa",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1581720426357,
    "updatedAt": 1581720426357,
    "author": {
      "username": "author-m61aty",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should create article with tags
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "tag_a",
      "tag_b"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-abvqic",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1581720426411,
    "updatedAt": 1581720426411,
    "author": {
      "username": "author-m61aty",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should disallow unauthenticated user
```
POST /articles

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should enforce required fields
```
POST /articles

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "title must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "description must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "body must be specified."
    ]
  }
}
```
## Get
### should get article by slug
```
GET /articles/title-2m3fsa
```
```
200 OK

{
  "article": {
    "createdAt": 1581720426357,
    "author": {
      "username": "author-m61aty",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-2m3fsa",
    "updatedAt": 1581720426357,
    "tagList": [],
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should get article with tags by slug
```
GET /articles/title-abvqic
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1581720426411,
    "author": {
      "username": "author-m61aty",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-abvqic",
    "updatedAt": 1581720426411,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should disallow unknown slug
```
GET /articles/470y5p
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [470y5p]"
    ]
  }
}
```
## Update
### should update article
```
PUT /articles/title-abvqic

{
  "article": {
    "title": "newtitle"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1581720426411,
    "author": {
      "username": "author-m61aty",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "newtitle",
    "body": "body",
    "slug": "title-abvqic",
    "updatedAt": 1581720426411,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
```
PUT /articles/title-abvqic

{
  "article": {
    "description": "newdescription"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1581720426411,
    "author": {
      "username": "author-m61aty",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "newdescription",
    "title": "newtitle",
    "body": "body",
    "slug": "title-abvqic",
    "updatedAt": 1581720426411,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
```
PUT /articles/title-abvqic

{
  "article": {
    "body": "newbody"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1581720426411,
    "author": {
      "username": "author-m61aty",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "newdescription",
    "title": "newtitle",
    "body": "newbody",
    "slug": "title-abvqic",
    "updatedAt": 1581720426411,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should disallow missing mutation
```
PUT /articles/title-abvqic

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article mutation must be specified."
    ]
  }
}
```
### should disallow empty mutation
```
PUT /articles/title-abvqic

{
  "article": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "At least one field must be specified: [title, description, article]."
    ]
  }
}
```
### should disallow unauthenticated update
```
PUT /articles/title-abvqic

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow updating non-existent article
```
PUT /articles/foo-title-abvqic

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foo-title-abvqic]"
    ]
  }
}
```
### should disallow non-author from updating
```
PUT /articles/title-abvqic

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article can only be updated by author: [author-m61aty]"
    ]
  }
}
```
## Favorite
### should favorite article
```
POST /articles/title-2m3fsa/favorite

{}
```
```
200 OK

{
  "article": {
    "createdAt": 1581720426357,
    "author": {
      "username": "author-m61aty",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-2m3fsa",
    "updatedAt": 1581720426357,
    "favoritedBy": [
      "non-author-1z1nzc"
    ],
    "favoritesCount": 1,
    "tagList": [],
    "favorited": true
  }
}
```
```
GET /articles/title-2m3fsa
```
```
200 OK

{
  "article": {
    "createdAt": 1581720426357,
    "author": {
      "username": "author-m61aty",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "favoritesCount": 1,
    "slug": "title-2m3fsa",
    "updatedAt": 1581720426357,
    "tagList": [],
    "favorited": true
  }
}
```
### should disallow favoriting by unauthenticated user
```
POST /articles/title-2m3fsa/favorite

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow favoriting unknown article
```
POST /articles/title-2m3fsa_foo/favorite

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [title-2m3fsa_foo]"
    ]
  }
}
```
### should unfavorite article
```
DELETE /articles/title-2m3fsa/favorite
```
```
200 OK

{
  "article": {
    "createdAt": 1581720426357,
    "author": {
      "username": "author-m61aty",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "favoritesCount": 0,
    "slug": "title-2m3fsa",
    "updatedAt": 1581720426357,
    "tagList": [],
    "favorited": false
  }
}
```
## Delete
### should delete article
```
DELETE /articles/title-2m3fsa
```
```
200 OK

{}
```
```
GET /articles/title-2m3fsa
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [title-2m3fsa]"
    ]
  }
}
```
### should disallow deleting by unauthenticated user
```
DELETE /articles/foo
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow deleting unknown article
```
DELETE /articles/foobar
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foobar]"
    ]
  }
}
```
### should disallow deleting article by non-author
```
DELETE /articles/title-abvqic
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article can only be deleted by author: [author-m61aty]"
    ]
  }
}
```
## List
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "ramnj0",
      "tag_0",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-3jpldd",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1581720427331,
    "updatedAt": 1581720427331,
    "author": {
      "username": "authoress-8ayl95",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "ramnj0",
      "tag_0",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "8va599",
      "tag_1",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-kcv382",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1581720427376,
    "updatedAt": 1581720427376,
    "author": {
      "username": "author-m61aty",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "8va599",
      "tag_1",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "dgyc74",
      "tag_2",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-w67y2z",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1581720427403,
    "updatedAt": 1581720427403,
    "author": {
      "username": "authoress-8ayl95",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "dgyc74",
      "tag_2",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "g3tuyt",
      "tag_3",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-v9w95z",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1581720427427,
    "updatedAt": 1581720427427,
    "author": {
      "username": "author-m61aty",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "g3tuyt",
      "tag_3",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "y84e01",
      "tag_4",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-3qj32m",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1581720427449,
    "updatedAt": 1581720427449,
    "author": {
      "username": "authoress-8ayl95",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "y84e01",
      "tag_4",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "cidri8",
      "tag_5",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-20hqld",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1581720427474,
    "updatedAt": 1581720427474,
    "author": {
      "username": "author-m61aty",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "cidri8",
      "tag_5",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "9xq3a5",
      "tag_6",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-kt39wx",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1581720427498,
    "updatedAt": 1581720427498,
    "author": {
      "username": "authoress-8ayl95",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "9xq3a5",
      "tag_6",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "7yylae",
      "tag_7",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-tzwber",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1581720427524,
    "updatedAt": 1581720427524,
    "author": {
      "username": "author-m61aty",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "7yylae",
      "tag_7",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "swf9ra",
      "tag_8",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-uifcpo",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1581720427552,
    "updatedAt": 1581720427552,
    "author": {
      "username": "authoress-8ayl95",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "swf9ra",
      "tag_8",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "tay5h6",
      "tag_9",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-maytfu",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1581720427580,
    "updatedAt": 1581720427580,
    "author": {
      "username": "author-m61aty",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "tay5h6",
      "tag_9",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "19y6ky",
      "tag_10",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-k9vs29",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1581720427610,
    "updatedAt": 1581720427610,
    "author": {
      "username": "authoress-8ayl95",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "19y6ky",
      "tag_10",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "n7cqcv",
      "tag_11",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-5nvavg",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1581720427633,
    "updatedAt": 1581720427633,
    "author": {
      "username": "author-m61aty",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "n7cqcv",
      "tag_11",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "hs0rp9",
      "tag_12",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-4kf390",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1581720427654,
    "updatedAt": 1581720427654,
    "author": {
      "username": "authoress-8ayl95",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "hs0rp9",
      "tag_12",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "48l8ed",
      "tag_13",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-jys4mr",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1581720427674,
    "updatedAt": 1581720427674,
    "author": {
      "username": "author-m61aty",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "48l8ed",
      "tag_13",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "m8rlpa",
      "tag_14",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-kv1d6a",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1581720427695,
    "updatedAt": 1581720427695,
    "author": {
      "username": "authoress-8ayl95",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "m8rlpa",
      "tag_14",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "8x3fax",
      "tag_15",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-p9uw0d",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1581720427715,
    "updatedAt": 1581720427715,
    "author": {
      "username": "author-m61aty",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "8x3fax",
      "tag_15",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "tsqwr6",
      "tag_16",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-1d509m",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1581720427739,
    "updatedAt": 1581720427739,
    "author": {
      "username": "authoress-8ayl95",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "tsqwr6",
      "tag_16",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "u4drin",
      "tag_17",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-oxmltx",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1581720427765,
    "updatedAt": 1581720427765,
    "author": {
      "username": "author-m61aty",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "u4drin",
      "tag_17",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "htrol6",
      "tag_18",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-w3ipgf",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1581720427790,
    "updatedAt": 1581720427790,
    "author": {
      "username": "authoress-8ayl95",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "htrol6",
      "tag_18",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "8z6xxr",
      "tag_19",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-s87dxa",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1581720427817,
    "updatedAt": 1581720427817,
    "author": {
      "username": "author-m61aty",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "8z6xxr",
      "tag_19",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should list articles
```
GET /articles
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "8z6xxr",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1581720427817,
      "author": {
        "username": "author-m61aty",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-s87dxa",
      "updatedAt": 1581720427817,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "htrol6",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1581720427790,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-w3ipgf",
      "updatedAt": 1581720427790,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "u4drin"
      ],
      "createdAt": 1581720427765,
      "author": {
        "username": "author-m61aty",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-oxmltx",
      "updatedAt": 1581720427765,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "tsqwr6"
      ],
      "createdAt": 1581720427739,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-1d509m",
      "updatedAt": 1581720427739,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "8x3fax",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1581720427715,
      "author": {
        "username": "author-m61aty",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-p9uw0d",
      "updatedAt": 1581720427715,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "m8rlpa",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1581720427695,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-kv1d6a",
      "updatedAt": 1581720427695,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "48l8ed",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1581720427674,
      "author": {
        "username": "author-m61aty",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-jys4mr",
      "updatedAt": 1581720427674,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "hs0rp9",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1581720427654,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-4kf390",
      "updatedAt": 1581720427654,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "n7cqcv",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1581720427633,
      "author": {
        "username": "author-m61aty",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-5nvavg",
      "updatedAt": 1581720427633,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "19y6ky",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1581720427610,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-k9vs29",
      "updatedAt": 1581720427610,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0",
        "tay5h6"
      ],
      "createdAt": 1581720427580,
      "author": {
        "username": "author-m61aty",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-maytfu",
      "updatedAt": 1581720427580,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "swf9ra",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1581720427552,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-uifcpo",
      "updatedAt": 1581720427552,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7yylae",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1581720427524,
      "author": {
        "username": "author-m61aty",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-tzwber",
      "updatedAt": 1581720427524,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "9xq3a5",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1581720427498,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-kt39wx",
      "updatedAt": 1581720427498,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "cidri8",
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1581720427474,
      "author": {
        "username": "author-m61aty",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-20hqld",
      "updatedAt": 1581720427474,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "y84e01"
      ],
      "createdAt": 1581720427449,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-3qj32m",
      "updatedAt": 1581720427449,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "g3tuyt",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1581720427427,
      "author": {
        "username": "author-m61aty",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-v9w95z",
      "updatedAt": 1581720427427,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dgyc74",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1581720427403,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-w67y2z",
      "updatedAt": 1581720427403,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "8va599",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1581720427376,
      "author": {
        "username": "author-m61aty",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-kcv382",
      "updatedAt": 1581720427376,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ramnj0",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1581720427331,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-3jpldd",
      "updatedAt": 1581720427331,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles with tag
```
GET /articles?tag=tag_7
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "7yylae",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1581720427524,
      "author": {
        "username": "author-m61aty",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-tzwber",
      "updatedAt": 1581720427524,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
GET /articles?tag=tag_mod_3_2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "u4drin"
      ],
      "createdAt": 1581720427765,
      "author": {
        "username": "author-m61aty",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-oxmltx",
      "updatedAt": 1581720427765,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "m8rlpa",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1581720427695,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-kv1d6a",
      "updatedAt": 1581720427695,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "n7cqcv",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1581720427633,
      "author": {
        "username": "author-m61aty",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-5nvavg",
      "updatedAt": 1581720427633,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "swf9ra",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1581720427552,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-uifcpo",
      "updatedAt": 1581720427552,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "cidri8",
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1581720427474,
      "author": {
        "username": "author-m61aty",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-20hqld",
      "updatedAt": 1581720427474,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dgyc74",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1581720427403,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-w67y2z",
      "updatedAt": 1581720427403,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles by author
```
GET /articles?author=authoress-8ayl95
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "htrol6",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1581720427790,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-w3ipgf",
      "updatedAt": 1581720427790,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "tsqwr6"
      ],
      "createdAt": 1581720427739,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-1d509m",
      "updatedAt": 1581720427739,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "m8rlpa",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1581720427695,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-kv1d6a",
      "updatedAt": 1581720427695,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "hs0rp9",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1581720427654,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-4kf390",
      "updatedAt": 1581720427654,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "19y6ky",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1581720427610,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-k9vs29",
      "updatedAt": 1581720427610,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "swf9ra",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1581720427552,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-uifcpo",
      "updatedAt": 1581720427552,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "9xq3a5",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1581720427498,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-kt39wx",
      "updatedAt": 1581720427498,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "y84e01"
      ],
      "createdAt": 1581720427449,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-3qj32m",
      "updatedAt": 1581720427449,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dgyc74",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1581720427403,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-w67y2z",
      "updatedAt": 1581720427403,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ramnj0",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1581720427331,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-3jpldd",
      "updatedAt": 1581720427331,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles favorited by user
```
GET /articles?favorited=non-author-1z1nzc
```
```
200 OK

{
  "articles": []
}
```
### should list articles by limit/offset
```
GET /articles?author=author-m61aty&limit=2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "8z6xxr",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1581720427817,
      "author": {
        "username": "author-m61aty",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-s87dxa",
      "updatedAt": 1581720427817,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "u4drin"
      ],
      "createdAt": 1581720427765,
      "author": {
        "username": "author-m61aty",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-oxmltx",
      "updatedAt": 1581720427765,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
GET /articles?author=author-m61aty&limit=2&offset=2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "8x3fax",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1581720427715,
      "author": {
        "username": "author-m61aty",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-p9uw0d",
      "updatedAt": 1581720427715,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "48l8ed",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1581720427674,
      "author": {
        "username": "author-m61aty",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-jys4mr",
      "updatedAt": 1581720427674,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles when authenticated
```
GET /articles
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "8z6xxr",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1581720427817,
      "author": {
        "username": "author-m61aty",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-s87dxa",
      "updatedAt": 1581720427817,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "htrol6",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1581720427790,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-w3ipgf",
      "updatedAt": 1581720427790,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "u4drin"
      ],
      "createdAt": 1581720427765,
      "author": {
        "username": "author-m61aty",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-oxmltx",
      "updatedAt": 1581720427765,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "tsqwr6"
      ],
      "createdAt": 1581720427739,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-1d509m",
      "updatedAt": 1581720427739,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "8x3fax",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1581720427715,
      "author": {
        "username": "author-m61aty",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-p9uw0d",
      "updatedAt": 1581720427715,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "m8rlpa",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1581720427695,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-kv1d6a",
      "updatedAt": 1581720427695,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "48l8ed",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1581720427674,
      "author": {
        "username": "author-m61aty",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-jys4mr",
      "updatedAt": 1581720427674,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "hs0rp9",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1581720427654,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-4kf390",
      "updatedAt": 1581720427654,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "n7cqcv",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1581720427633,
      "author": {
        "username": "author-m61aty",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-5nvavg",
      "updatedAt": 1581720427633,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "19y6ky",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1581720427610,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-k9vs29",
      "updatedAt": 1581720427610,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0",
        "tay5h6"
      ],
      "createdAt": 1581720427580,
      "author": {
        "username": "author-m61aty",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-maytfu",
      "updatedAt": 1581720427580,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "swf9ra",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1581720427552,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-uifcpo",
      "updatedAt": 1581720427552,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7yylae",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1581720427524,
      "author": {
        "username": "author-m61aty",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-tzwber",
      "updatedAt": 1581720427524,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "9xq3a5",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1581720427498,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-kt39wx",
      "updatedAt": 1581720427498,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "cidri8",
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1581720427474,
      "author": {
        "username": "author-m61aty",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-20hqld",
      "updatedAt": 1581720427474,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "y84e01"
      ],
      "createdAt": 1581720427449,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-3qj32m",
      "updatedAt": 1581720427449,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "g3tuyt",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1581720427427,
      "author": {
        "username": "author-m61aty",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-v9w95z",
      "updatedAt": 1581720427427,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dgyc74",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1581720427403,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-w67y2z",
      "updatedAt": 1581720427403,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "8va599",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1581720427376,
      "author": {
        "username": "author-m61aty",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-kcv382",
      "updatedAt": 1581720427376,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ramnj0",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1581720427331,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-3jpldd",
      "updatedAt": 1581720427331,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should disallow multiple of author/tag/favorited
```
GET /articles?tag=foo&author=bar
```
```
GET /articles?author=foo&favorited=bar
```
```
GET /articles?favorited=foo&tag=bar
```
## Feed
### should get feed
```
GET /articles/feed
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
200 OK

{
  "articles": []
}
```
```
POST /profiles/authoress-8ayl95/follow

{}
```
```
200 OK

{
  "profile": {
    "username": "authoress-8ayl95",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /articles/feed
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "htrol6",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1581720427790,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-w3ipgf",
      "updatedAt": 1581720427790,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "tsqwr6"
      ],
      "createdAt": 1581720427739,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-1d509m",
      "updatedAt": 1581720427739,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "m8rlpa",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1581720427695,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-kv1d6a",
      "updatedAt": 1581720427695,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "hs0rp9",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1581720427654,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-4kf390",
      "updatedAt": 1581720427654,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "19y6ky",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1581720427610,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-k9vs29",
      "updatedAt": 1581720427610,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "swf9ra",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1581720427552,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-uifcpo",
      "updatedAt": 1581720427552,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "9xq3a5",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1581720427498,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-kt39wx",
      "updatedAt": 1581720427498,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "y84e01"
      ],
      "createdAt": 1581720427449,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-3qj32m",
      "updatedAt": 1581720427449,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dgyc74",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1581720427403,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-w67y2z",
      "updatedAt": 1581720427403,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ramnj0",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1581720427331,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-3jpldd",
      "updatedAt": 1581720427331,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
POST /profiles/author-m61aty/follow

{}
```
```
200 OK

{
  "profile": {
    "username": "author-m61aty",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /articles/feed
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "8z6xxr",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1581720427817,
      "author": {
        "username": "author-m61aty",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-s87dxa",
      "updatedAt": 1581720427817,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "htrol6",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1581720427790,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-w3ipgf",
      "updatedAt": 1581720427790,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "u4drin"
      ],
      "createdAt": 1581720427765,
      "author": {
        "username": "author-m61aty",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-oxmltx",
      "updatedAt": 1581720427765,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "tsqwr6"
      ],
      "createdAt": 1581720427739,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-1d509m",
      "updatedAt": 1581720427739,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "8x3fax",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1581720427715,
      "author": {
        "username": "author-m61aty",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-p9uw0d",
      "updatedAt": 1581720427715,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "m8rlpa",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1581720427695,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-kv1d6a",
      "updatedAt": 1581720427695,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "48l8ed",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1581720427674,
      "author": {
        "username": "author-m61aty",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-jys4mr",
      "updatedAt": 1581720427674,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "hs0rp9",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1581720427654,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-4kf390",
      "updatedAt": 1581720427654,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "n7cqcv",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1581720427633,
      "author": {
        "username": "author-m61aty",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-5nvavg",
      "updatedAt": 1581720427633,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "19y6ky",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1581720427610,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-k9vs29",
      "updatedAt": 1581720427610,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0",
        "tay5h6"
      ],
      "createdAt": 1581720427580,
      "author": {
        "username": "author-m61aty",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-maytfu",
      "updatedAt": 1581720427580,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "swf9ra",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1581720427552,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-uifcpo",
      "updatedAt": 1581720427552,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7yylae",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1581720427524,
      "author": {
        "username": "author-m61aty",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-tzwber",
      "updatedAt": 1581720427524,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "9xq3a5",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1581720427498,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-kt39wx",
      "updatedAt": 1581720427498,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "cidri8",
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1581720427474,
      "author": {
        "username": "author-m61aty",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-20hqld",
      "updatedAt": 1581720427474,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "y84e01"
      ],
      "createdAt": 1581720427449,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-3qj32m",
      "updatedAt": 1581720427449,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "g3tuyt",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1581720427427,
      "author": {
        "username": "author-m61aty",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-v9w95z",
      "updatedAt": 1581720427427,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dgyc74",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1581720427403,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-w67y2z",
      "updatedAt": 1581720427403,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "8va599",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1581720427376,
      "author": {
        "username": "author-m61aty",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-kcv382",
      "updatedAt": 1581720427376,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ramnj0",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1581720427331,
      "author": {
        "username": "authoress-8ayl95",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-3jpldd",
      "updatedAt": 1581720427331,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should disallow unauthenticated feed
```
GET /articles/feed
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
## Tags
### should get tags
```
GET /tags
```
```
200 OK

{
  "tags": [
    "9xq3a5",
    "tag_6",
    "tag_mod_2_0",
    "tag_mod_3_0",
    "tag_a",
    "tag_b",
    "8va599",
    "tag_1",
    "tag_mod_2_1",
    "tag_mod_3_1",
    "hs0rp9",
    "tag_12",
    "htrol6",
    "tag_18",
    "8z6xxr",
    "tag_19",
    "dgyc74",
    "tag_2",
    "tag_mod_3_2",
    "m8rlpa",
    "tag_14",
    "48l8ed",
    "tag_13",
    "tag_4",
    "y84e01",
    "ramnj0",
    "tag_0",
    "swf9ra",
    "tag_8",
    "8x3fax",
    "tag_15",
    "tag_17",
    "u4drin",
    "tag_9",
    "tay5h6",
    "19y6ky",
    "tag_10",
    "g3tuyt",
    "tag_3",
    "7yylae",
    "tag_7",
    "tag_16",
    "tsqwr6",
    "n7cqcv",
    "tag_11",
    "cidri8",
    "tag_5"
  ]
}
```
# Comment
```
POST /users

{
  "user": {
    "email": "author-eof7uc@email.com",
    "username": "author-eof7uc",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "author-eof7uc@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvci1lb2Y3dWMiLCJpYXQiOjE1ODE3MjA0MjksImV4cCI6MTU4MTg5MzIyOX0.NpTVj34eXIBDyvnt19ecmMzlwMriOzFM9nPp8Q0RDQE",
    "username": "author-eof7uc",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "commenter-h9ju69@email.com",
    "username": "commenter-h9ju69",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "commenter-h9ju69@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImNvbW1lbnRlci1oOWp1NjkiLCJpYXQiOjE1ODE3MjA0MjksImV4cCI6MTU4MTg5MzIyOX0.ydJwqfxgJ0polqW90pHPL4ROLtyLwF6zfGJaDjZ70dA",
    "username": "commenter-h9ju69",
    "bio": "",
    "image": ""
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body"
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-9cwai3",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1581720429262,
    "updatedAt": 1581720429262,
    "author": {
      "username": "author-eof7uc",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
## Create
### should create comment
```
POST /articles/title-9cwai3/comments

{
  "comment": {
    "body": "test comment fd8762"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "66a6dad7-8d52-4048-8907-52348fc4a50a",
    "slug": "title-9cwai3",
    "body": "test comment fd8762",
    "createdAt": 1581720429290,
    "updatedAt": 1581720429290,
    "author": {
      "username": "commenter-h9ju69",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-9cwai3/comments

{
  "comment": {
    "body": "test comment u7o9fn"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "aa4da829-0047-471a-bff3-cca383f6105f",
    "slug": "title-9cwai3",
    "body": "test comment u7o9fn",
    "createdAt": 1581720429327,
    "updatedAt": 1581720429327,
    "author": {
      "username": "commenter-h9ju69",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-9cwai3/comments

{
  "comment": {
    "body": "test comment kf6g9k"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "8ff63247-aef9-42fb-8a7d-1eea22b3f6b5",
    "slug": "title-9cwai3",
    "body": "test comment kf6g9k",
    "createdAt": 1581720429361,
    "updatedAt": 1581720429361,
    "author": {
      "username": "commenter-h9ju69",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-9cwai3/comments

{
  "comment": {
    "body": "test comment oyndrv"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "321221d9-a20e-4b33-b6d9-0add64b47173",
    "slug": "title-9cwai3",
    "body": "test comment oyndrv",
    "createdAt": 1581720429402,
    "updatedAt": 1581720429402,
    "author": {
      "username": "commenter-h9ju69",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-9cwai3/comments

{
  "comment": {
    "body": "test comment bldysp"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "77bb19da-4d5a-4af6-b592-a0a26b93f4fa",
    "slug": "title-9cwai3",
    "body": "test comment bldysp",
    "createdAt": 1581720429429,
    "updatedAt": 1581720429429,
    "author": {
      "username": "commenter-h9ju69",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-9cwai3/comments

{
  "comment": {
    "body": "test comment o51sdc"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "69c15ffc-a92b-47ea-aa53-1ec195c1b8ff",
    "slug": "title-9cwai3",
    "body": "test comment o51sdc",
    "createdAt": 1581720429457,
    "updatedAt": 1581720429457,
    "author": {
      "username": "commenter-h9ju69",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-9cwai3/comments

{
  "comment": {
    "body": "test comment 8npas0"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "5851ad67-751e-447d-bba4-a48733515af6",
    "slug": "title-9cwai3",
    "body": "test comment 8npas0",
    "createdAt": 1581720429478,
    "updatedAt": 1581720429478,
    "author": {
      "username": "commenter-h9ju69",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-9cwai3/comments

{
  "comment": {
    "body": "test comment 4s5zef"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "43232707-6aa3-4151-b6c6-d8e1b70d7d89",
    "slug": "title-9cwai3",
    "body": "test comment 4s5zef",
    "createdAt": 1581720429505,
    "updatedAt": 1581720429505,
    "author": {
      "username": "commenter-h9ju69",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-9cwai3/comments

{
  "comment": {
    "body": "test comment z9t8hz"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "39655129-b6af-4175-adb2-2b3dc4d3bebf",
    "slug": "title-9cwai3",
    "body": "test comment z9t8hz",
    "createdAt": 1581720429540,
    "updatedAt": 1581720429540,
    "author": {
      "username": "commenter-h9ju69",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-9cwai3/comments

{
  "comment": {
    "body": "test comment azd9fs"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "2f9c2b2b-b82d-45b2-867d-04f2e5a22d8f",
    "slug": "title-9cwai3",
    "body": "test comment azd9fs",
    "createdAt": 1581720429562,
    "updatedAt": 1581720429562,
    "author": {
      "username": "commenter-h9ju69",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
### should disallow unauthenticated user
```
POST /articles/title-9cwai3/comments

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should enforce comment body
```
POST /articles/title-9cwai3/comments

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Comment must be specified."
    ]
  }
}
```
### should disallow non-existent article
```
POST /articles/foobar/comments

{
  "comment": {
    "body": "test comment gceqg1"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foobar]"
    ]
  }
}
```
## Get
### should get all comments for article
```
GET /articles/title-9cwai3/comments
```
```
200 OK

{
  "comments": [
    {
      "createdAt": 1581720429562,
      "id": "2f9c2b2b-b82d-45b2-867d-04f2e5a22d8f",
      "body": "test comment azd9fs",
      "slug": "title-9cwai3",
      "author": {
        "username": "commenter-h9ju69",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1581720429562
    },
    {
      "createdAt": 1581720429478,
      "id": "5851ad67-751e-447d-bba4-a48733515af6",
      "body": "test comment 8npas0",
      "slug": "title-9cwai3",
      "author": {
        "username": "commenter-h9ju69",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1581720429478
    },
    {
      "createdAt": 1581720429540,
      "id": "39655129-b6af-4175-adb2-2b3dc4d3bebf",
      "body": "test comment z9t8hz",
      "slug": "title-9cwai3",
      "author": {
        "username": "commenter-h9ju69",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1581720429540
    },
    {
      "createdAt": 1581720429457,
      "id": "69c15ffc-a92b-47ea-aa53-1ec195c1b8ff",
      "body": "test comment o51sdc",
      "slug": "title-9cwai3",
      "author": {
        "username": "commenter-h9ju69",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1581720429457
    },
    {
      "createdAt": 1581720429361,
      "id": "8ff63247-aef9-42fb-8a7d-1eea22b3f6b5",
      "body": "test comment kf6g9k",
      "slug": "title-9cwai3",
      "author": {
        "username": "commenter-h9ju69",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1581720429361
    },
    {
      "createdAt": 1581720429505,
      "id": "43232707-6aa3-4151-b6c6-d8e1b70d7d89",
      "body": "test comment 4s5zef",
      "slug": "title-9cwai3",
      "author": {
        "username": "commenter-h9ju69",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1581720429505
    },
    {
      "createdAt": 1581720429429,
      "id": "77bb19da-4d5a-4af6-b592-a0a26b93f4fa",
      "body": "test comment bldysp",
      "slug": "title-9cwai3",
      "author": {
        "username": "commenter-h9ju69",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1581720429429
    },
    {
      "createdAt": 1581720429290,
      "id": "66a6dad7-8d52-4048-8907-52348fc4a50a",
      "body": "test comment fd8762",
      "slug": "title-9cwai3",
      "author": {
        "username": "commenter-h9ju69",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1581720429290
    },
    {
      "createdAt": 1581720429327,
      "id": "aa4da829-0047-471a-bff3-cca383f6105f",
      "body": "test comment u7o9fn",
      "slug": "title-9cwai3",
      "author": {
        "username": "commenter-h9ju69",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1581720429327
    },
    {
      "createdAt": 1581720429402,
      "id": "321221d9-a20e-4b33-b6d9-0add64b47173",
      "body": "test comment oyndrv",
      "slug": "title-9cwai3",
      "author": {
        "username": "commenter-h9ju69",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1581720429402
    }
  ]
}
```
## Delete
### should delete comment
```
DELETE /articles/title-9cwai3/comments/66a6dad7-8d52-4048-8907-52348fc4a50a
```
```
200 OK

{}
```
### only comment author should be able to delete comment
```
DELETE /articles/title-9cwai3/comments/aa4da829-0047-471a-bff3-cca383f6105f
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only comment author can delete: [commenter-h9ju69]"
    ]
  }
}
```
### should disallow unauthenticated user
```
DELETE /articles/title-9cwai3/comments/aa4da829-0047-471a-bff3-cca383f6105f
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow deleting unknown comment
```
DELETE /articles/title-9cwai3/comments/foobar_id
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Comment ID not found: [foobar_id]"
    ]
  }
}
```
# User
## Create
### should create user
```
POST /users

{
  "user": {
    "email": "user1-0.vybafkjrca@email.com",
    "username": "user1-0.vybafkjrca",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user1-0.vybafkjrca@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAudnliYWZranJjYSIsImlhdCI6MTU4MTcyMDQyOSwiZXhwIjoxNTgxODkzMjI5fQ.nsmaWcYrHMQlGWCorvbNU3hDAZgRF0MZsrG6n4MWr0A",
    "username": "user1-0.vybafkjrca",
    "bio": "",
    "image": ""
  }
}
```
### should disallow same username
```
POST /users

{
  "user": {
    "email": "user1-0.vybafkjrca@email.com",
    "username": "user1-0.vybafkjrca",
    "password": "password"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Username already taken: [user1-0.vybafkjrca]"
    ]
  }
}
```
### should disallow same email
```
POST /users

{
  "user": {
    "username": "user2",
    "email": "user1-0.vybafkjrca@email.com",
    "password": "password"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email already taken: [user1-0.vybafkjrca@email.com]"
    ]
  }
}
```
### should enforce required fields
```
POST /users

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "foo": 1
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Username must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "username": 1
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "username": 1,
    "email": 2
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Password must be specified."
    ]
  }
}
```
## Login
### should login
```
POST /users/login

{
  "user": {
    "email": "user1-0.vybafkjrca@email.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user1-0.vybafkjrca@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAudnliYWZranJjYSIsImlhdCI6MTU4MTcyMDQyOSwiZXhwIjoxNTgxODkzMjI5fQ.nsmaWcYrHMQlGWCorvbNU3hDAZgRF0MZsrG6n4MWr0A",
    "username": "user1-0.vybafkjrca",
    "bio": "",
    "image": ""
  }
}
```
### should disallow unknown email
```
POST /users/login

{
  "user": {
    "email": "0.hqd3d8hs6r6",
    "password": "somepassword"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email not found: [0.hqd3d8hs6r6]"
    ]
  }
}
```
### should disallow wrong password
```
POST /users/login

{
  "user": {
    "email": "user1-0.vybafkjrca@email.com",
    "password": "0.m5r3tedzprd"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Wrong password."
    ]
  }
}
```
### should enforce required fields
```
POST /users/login

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
```
POST /users/login

{
  "user": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email must be specified."
    ]
  }
}
```
```
POST /users/login

{
  "user": {
    "email": "someemail"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Password must be specified."
    ]
  }
}
```
## Get
### should get current user
```
GET /user
```
```
200 OK

{
  "user": {
    "email": "user1-0.vybafkjrca@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAudnliYWZranJjYSIsImlhdCI6MTU4MTcyMDQyOSwiZXhwIjoxNTgxODkzMjI5fQ.nsmaWcYrHMQlGWCorvbNU3hDAZgRF0MZsrG6n4MWr0A",
    "username": "user1-0.vybafkjrca",
    "bio": "",
    "image": ""
  }
}
```
### should disallow bad tokens
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
## Profile
### should get profile
```
GET /profiles/user1-0.vybafkjrca
```
```
200 OK

{
  "profile": {
    "username": "user1-0.vybafkjrca",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
### should disallow unknown username
```
GET /profiles/foo_0.3qtya61vbw4
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User not found: [foo_0.3qtya61vbw4]"
    ]
  }
}
```
### should follow/unfollow user
```
POST /users

{
  "user": {
    "username": "followed_user",
    "email": "followed_user@mail.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "followed_user@mail.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImZvbGxvd2VkX3VzZXIiLCJpYXQiOjE1ODE3MjA0MzAsImV4cCI6MTU4MTg5MzIzMH0.ZcDZ_tAHNeOtJBT3tIGeHcuutbHwIRmtJWWLbbPBtQM",
    "username": "followed_user",
    "bio": "",
    "image": ""
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /profiles/followed_user
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /profiles/followed_user
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
POST /users

{
  "user": {
    "username": "user2-0.s90j27vss5m",
    "email": "user2-0.s90j27vss5m@mail.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user2-0.s90j27vss5m@mail.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIyLTAuczkwajI3dnNzNW0iLCJpYXQiOjE1ODE3MjA0MzAsImV4cCI6MTU4MTg5MzIzMH0.hk5AET_lwdck4BRGBkzRz8s6RlKkBXQlEqUuWL8ga1U",
    "username": "user2-0.s90j27vss5m",
    "bio": "",
    "image": ""
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
### should disallow following with bad token
```
POST /profiles/followed_user/follow
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
## Update
### should update user
```
PUT /user

{
  "user": {
    "email": "updated-user1-0.vybafkjrca@email.com"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.vybafkjrca",
    "email": "updated-user1-0.vybafkjrca@email.com",
    "image": "",
    "bio": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAudnliYWZranJjYSIsImlhdCI6MTU4MTcyMDQyOSwiZXhwIjoxNTgxODkzMjI5fQ.nsmaWcYrHMQlGWCorvbNU3hDAZgRF0MZsrG6n4MWr0A"
  }
}
```
```
PUT /user

{
  "user": {
    "password": "newpassword"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.vybafkjrca",
    "email": "updated-user1-0.vybafkjrca@email.com",
    "image": "",
    "bio": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAudnliYWZranJjYSIsImlhdCI6MTU4MTcyMDQyOSwiZXhwIjoxNTgxODkzMjI5fQ.nsmaWcYrHMQlGWCorvbNU3hDAZgRF0MZsrG6n4MWr0A"
  }
}
```
```
PUT /user

{
  "user": {
    "bio": "newbio"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.vybafkjrca",
    "bio": "newbio",
    "image": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAudnliYWZranJjYSIsImlhdCI6MTU4MTcyMDQyOSwiZXhwIjoxNTgxODkzMjI5fQ.nsmaWcYrHMQlGWCorvbNU3hDAZgRF0MZsrG6n4MWr0A"
  }
}
```
```
PUT /user

{
  "user": {
    "image": "newimage"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.vybafkjrca",
    "image": "newimage",
    "bio": "newbio",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAudnliYWZranJjYSIsImlhdCI6MTU4MTcyMDQyOSwiZXhwIjoxNTgxODkzMjI5fQ.nsmaWcYrHMQlGWCorvbNU3hDAZgRF0MZsrG6n4MWr0A"
  }
}
```
### should disallow missing token/email in update
```
PUT /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
PUT /user

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
### should disallow reusing email
```
POST /users

{
  "user": {
    "email": "user2-0.j7alr7jw9rk@email.com",
    "username": "user2-0.j7alr7jw9rk",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user2-0.j7alr7jw9rk@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIyLTAuajdhbHI3anc5cmsiLCJpYXQiOjE1ODE3MjA0MzAsImV4cCI6MTU4MTg5MzIzMH0.hLT1IoVwiVvbXlBA3FMkVIeWY7sebhkQ1pdTh_TC0uY",
    "username": "user2-0.j7alr7jw9rk",
    "bio": "",
    "image": ""
  }
}
```
```
PUT /user

{
  "user": {
    "email": "user2-0.j7alr7jw9rk@email.com"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email already taken: [user2-0.j7alr7jw9rk@email.com]"
    ]
  }
}
```
# Util
## Ping
### should ping
```
GET /ping
```
```
200 OK

{
  "pong": "2020-02-14T22:47:10.434Z",
  "AWS_REGION": "us-east-1",
  "DYNAMODB_NAMESPACE": "dev"
}
```
