## Todo Server

### Prerequisite

- Install [Docker](https://www.docker.com/)

### How to run the server

```bash
docker compose up --build
```

### API urls

Express(REST API) server  is running on port `8080`

#### schema
```typescript
interface Todo {
  // todo item id
  id: string;
  // todo item title
  title: string;
  // you can ignore this field at this moment
  description?: string;
  // todo item status (is it completed or not)
  completed: boolean;
  // todo item status (is it archived or not)
  archived: boolean;
  // todo item created date
  createdAt: string;
  // todo item updated date
  updatedAt: string;
}
```

#### endpoints

1. `GET /api/todos` - Get all todos

**Example**
```typescript
fetch(`http://localhost:8080/api/todos`, {
  method: 'GET'
})
  .then((response) => response.json())
  .then((todos) => {
    // result is an array of todo item
    console.log('todos', todos)
  })
```

2. `POST /api/todos` - Add todo

**Payload**

- title: string (required)

**Example**
```typescript
fetch(`http://localhost:8080/api/todos`, {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({ title: 'hello' })
})
  .then((response) => response.json())
  .then((createdTodo) => {
    // result is created todo item
    console.log('createdTodo', createdTodo)
  })
```

3. `PUT /api/todos/:todoId` - Update todo

**Payload**

- title: string (optional)
- archived: boolean (optional)
- completed: boolean (optional)

**Example**
```typescript
fetch(`http://localhost:8080/api/todos/496`, {
  method: 'PUT',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({ archived: false })
})
  .then((response) => response.json())
  .then((updatedTodo) => {
    // result is updated todo item
    console.log('updatedTodo', updatedTodo)
  })
```

4. `DELETE /api/todos/:todoId` - Delete todo

**Example**
```typescript
fetch(`http://localhost:8080/api/todos/496`, {
  method: 'DELETE'
})
  .then((response) => response.json())
  .then((deletedTodo) => {
    // result is deleted todo item
    console.log('deletedTodo', deletedTodo)
  })
```
