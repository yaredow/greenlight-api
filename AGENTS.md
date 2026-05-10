# Greenlight - Go REST API

## Project Structure
- `cmd/api/` - Main application entry point
- `internal/data/` - Database models and operations
- `internal/validator/` - Input validation
- `migrations/` - SQL migrations (use golang-migrate/migrate tool)

## Commands

### Run the API
```bash
go run ./cmd/api
# Or with env var:
GREENLIGHT_DB_DSN="postgres://user:pass@localhost/greenlight?sslmode=disable" go run ./cmd/api
```

### Build
```bash
go build ./cmd/api
```

### Run Migrations
```bash
# Up migrations
migrate -path=./migrations -database=$GREENLIGHT_DB_DSN up

# Down migrations
migrate -path=./migrations -database=$GREENLIGHT_DB_DSN down
```

### Database Permissions
If you get "permission denied for schema public", grant permissions:
```bash
psql -U <user> -d <db> -c "GRANT ALL ON SCHEMA public TO <user>;"
```

## Runtime JSON Format
The `Runtime` type in `internal/data/runtime.go` accepts both:
- Plain integer: `{"runtime": 180}`
- String format: `{"runtime": "180 mins"}`

## Key Files
- `cmd/api/main.go` - Entry point, server config
- `cmd/api/routes.go` - HTTP route definitions
- `cmd/api/movies.go` - Movie handlers
- `internal/data/runtime.go` - Runtime type with JSON marshaling