# System Architecture Design

## Frontend Layer
```javascript
// React component pattern
const Button = ({ variant = 'primary', children }) => (
  <button className={`btn btn-${variant}`}>
    {children}
  </button>
);
```

## Backend Layer
```java
// Spring Boot service pattern
@Service
public class UserService {
    @Autowired
    private UserRepository repository;
    
    public User getUserById(Long id) {
        return repository.findById(id)
            .orElseThrow(() -> new UserNotFoundException(id));
    }
}
```

## Database Layer
```sql
-- PostgreSQL schema design
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    username VARCHAR(50) UNIQUE NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

## API Design
```typescript
// TypeScript interface for API contracts
interface APIResponse<T> {
    data: T;
    status: 'success' | 'error';
    message?: string;
    timestamp: Date;
}

interface User {
    id: number;
    name: string;
    email: string;
}
```

## Configuration
```yaml
# application.yml
spring:
  datasource:
    url: jdbc:postgresql://localhost:5432/mydb
    username: admin
    password: secret
```

## Infrastructure
```dockerfile
# Dockerfile multi-stage build
FROM node:18-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

FROM nginx:alpine
COPY --from=builder /app/build /usr/share/nginx/html
EXPOSE 80
```
