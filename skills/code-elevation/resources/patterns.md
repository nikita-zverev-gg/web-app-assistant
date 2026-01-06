# Pattern Reference

## State Management {#state}

### Props Drilling (Startup)

```tsx
// Passing props through 5 levels
<App user={user}>
  <Layout user={user}>
    <Sidebar user={user}>
      <UserInfo user={user} />
    </Sidebar>
  </Layout>
</App>
```

### Centralized State (Enterprise)

```tsx
// Zustand store
const useUserStore = create((set) => ({
  user: null,
  setUser: (user) => set({ user })
}))

// Usage anywhere in the tree
const UserInfo = () => {
  const user = useUserStore((state) => state.user)
  return <div>{user?.name}</div>
}
```

**Citation**: [Zustand docs](https://zustand-demo.pmnd.rs/)

## Error Handling {#errors}

### Console.log (Startup)

```ts
try {
  await api.call()
} catch (e) {
  console.log(e)
}
```

### Structured (Enterprise)

```ts
import { logger } from '@gg/logger'
import { AppError } from '@gg/errors'

try {
  await api.call()
} catch (e) {
  logger.error('API call failed', { error: e, context })
  throw new AppError('OPERATION_FAILED', e)
}
```

**Citation**: [Node.js error handling](https://nodejs.org/api/errors.html)

## API Design {#api}

### Mixed Conventions (Startup)

```ts
// Inconsistent naming and response shapes
app.get('/getUsers', ...)
app.post('/user/create', ...)
app.delete('/remove-user/:id', ...)
```

### Consistent GraphQL (Enterprise)

```graphql
type Query {
  users(where: UserFilter): [User!]!
  user(id: ID!): User
}

type Mutation {
  createUser(input: CreateUserInput!): User!
  updateUser(id: ID!, input: UpdateUserInput!): User!
  deleteUser(id: ID!): Boolean!
}
```

**Citation**: See GraphQL best practices in project docs

## Testing Patterns {#testing}

### No Tests (Startup)

```ts
// Ship fast, fix later
export function calculateTotal(items) {
  return items.reduce((sum, item) => sum + item.price, 0)
}
```

### TDD (Enterprise)

```ts
// Test first
describe('calculateTotal', () => {
  it('returns 0 for empty array', () => {
    expect(calculateTotal([])).toBe(0)
  })

  it('sums item prices', () => {
    const items = [{ price: 10 }, { price: 20 }]
    expect(calculateTotal(items)).toBe(30)
  })
})
```
