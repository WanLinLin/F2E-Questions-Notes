# Normalizing State Shape

將client端的state也當作資料庫來看待，把多處重複的資料結構改成資料庫的實體模型

```js
const originalResponse = [
  {
    id : "post1",
    author : {username : "user1", name : "User 1"},
    body : "......",
    comments : [
      {
        id : "comment1",
        author : {username : "user2", name : "User 2"},
        comment : ".....",
      },
      {
        id : "comment2",
        author : {username : "user3", name : "User 3"},
        comment : ".....",
      }
    ]
  },
  {
    id : "post2",
    author : {username : "user2", name : "User 2"},
    body : "......",
    comments : [
      {
        id : "comment3",
        author : {username : "user3", name : "User 3"},
        comment : ".....",
      },
      {
        id : "comment4",
        author : {username : "user1", name : "User 1"},
        comment : ".....",
      },
      {
        id : "comment5",
        author : {username : "user3", name : "User 3"},
        comment : ".....",
      }
    ]    
  }
]
```

```js
const normalizedState = {
  posts : {
    byId : {
      "post1" : {
        id : "post1",
        author : "user1",
        body : "......",
        comments : ["comment1", "comment2"]    
      },
      "post2" : {
        id : "post2",
        author : "user2",
        body : "......",
        comments : ["comment3", "comment4", "comment5"]    
      }
    }
    allIds : ["post1", "post2"]
  },
  comments : {
    byId : {
      "comment1" : {
        id : "comment1",
        author : "user2",
        comment : ".....",
      },
      "comment2" : {
        id : "comment2",
        author : "user3",
        comment : ".....",
      },
      "comment3" : {
        id : "comment3",
        author : "user3",
        comment : ".....",
      },
      "comment4" : {
        id : "comment4",
        author : "user1",
        comment : ".....",
      },
      "comment5" : {
        id : "comment5",
        author : "user3",
        comment : ".....",
      },
    },
    allIds : ["comment1", "comment2", "comment3", "commment4", "comment5"]
  },
  users : {
    byId : {
      "user1" : {
        username : "user1",
        name : "User 1",
      }
      "user2" : {
        username : "user2",
        name : "User 2",
      }
      "user3" : {
        username : "user3",
        name : "User 3",
      }
    },
    allIds : ["user1", "user2", "user3"]
  }
}
```

通常會將可以獨自成為一張資料表的資料放在state的entities中：

```js
{
  simpleDomainData1: {....},
  simpleDomainData2: {....}
  entities : {
    entityType1 : {....},
    entityType2 : {....}
  }
  ui : {
    uiSection1 : {....},
    uiSection2 : {....}
  }
}
```

## Normalizr

normalizr是一個會將JSON data依照指定的schema正規化資料的node lib


```js
import { normalize, schema } from 'normalizr';

// 使用schema定義資料表以及資料表關聯
const user = new schema.Entity('users');

const comment = new schema.Entity('comments', {
  commenter: user
});

const article = new schema.Entity('articles', { 
  author: user,
  comments: [ comment ]
});

// 使用normalize將raw data根據schema正規化
const normalizedData = normalize(originalData, article);
```

## Reference
- http://redux.js.org/docs/recipes/reducers/NormalizingStateShape.html
- http://redux.js.org/docs/recipes/reducers/UpdatingNormalizedData.html
- https://github.com/paularmstrong/normalizr