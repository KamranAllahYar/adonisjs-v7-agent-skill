---
name: adonisjs-v7-agent
description: Comprehensive AdonisJS v7 documentation agent skill. Use when working with AdonisJS v7 projects, understanding framework capabilities, writing code, fixing bugs, or answering questions about the AdonisJS v7 ecosystem. Compatible with Claude Code, OpenCode, Codex, and other Claude-based AI coding assistants.
---

# AdonisJS v7 Agent Skill

This skill provides comprehensive knowledge of AdonisJS v7 for AI agents working with the framework.

## When to Use This Skill

Use this skill when the user:
- Asks about AdonisJS v7 features, packages, or capabilities
- Needs to build, debug, or modify an AdonisJS v7 application
- Asks how to implement specific functionality in AdonisJS
- Asks about routing, controllers, models, authentication, etc.
- Needs to reference official documentation
- Asks about upgrading from AdonisJS v5/v6 to v7
- Is learning AdonisJS and needs guidance

## Quick Reference

| Task | Docs Link |
|------|-----------|
| Routing | https://docs.adonisjs.com/guides/basics/routing |
| Controllers | https://docs.adonisjs.com/guides/basics/controllers |
| Models (Lucid) | https://docs.adonisjs.com/guides/database/lucid |
| Authentication | https://docs.adonisjs.com/guides/auth/introduction |
| Validation | https://docs.adonisjs.com/guides/basics/validation |
| Middleware | https://docs.adonisjs.com/guides/basics/middleware |
| Testing | https://docs.adonisjs.com/guides/testing/introduction |
| Deployment | https://docs.adonisjs.com/start/deployment |

## Base Documentation URL

All documentation references should be prefixed with: **https://docs.adonisjs.com/**

Example: For routing docs, link to https://docs.adonisjs.com/guides/basics/routing

## Project Structure

An AdonisJS v7 project has this structure:

```
├── app/                    # Application code
│   ├── controllers/        # HTTP request handlers
│   ├── models/             # Database models (Lucid)
│   ├── services/           # Business logic services
│   ├── middleware/         # HTTP middleware
│   ├── validators/         # Request validation
│   ├── exceptions/         # Custom exception classes
│   └── mailers/            # Email handlers
├── bin/                    # CLI entry points
├── config/                 # Configuration files
├── database/
│   ├── migrations/        # Schema migrations
│   ├── seeders/          # Test data seeding
│   └── factories/         # Test data factories
├── resources/             # Frontend assets/views
├── start/                 # Bootstrap files
│   ├── routes.ts         # Route definitions
│   ├── kernel.ts         # Middleware registration
│   └── env.ts            # Environment variables
├── tests/                 # Test files
├── ace.js                # Ace CLI entry point
├── adonisrc.ts           # AdonisJS config
└── vite.config.ts        # Vite bundler config
```

## Key Packages

| Package | Purpose | Docs Link |
|---------|---------|-----------|
| `@adonisjs/core` | Core framework | https://docs.adonisjs.com/reference/application |
| `@adonisjs/lucid` | SQL ORM | https://docs.adonisjs.com/guides/database/lucid |
| `@adonisjs/auth` | Authentication | https://docs.adonisjs.com/guides/auth/introduction |
| `@adonisjs/session` | Sessions | https://docs.adonisjs.com/guides/basics/session |
| `@adonisjs/validator` | Validation | https://docs.adonisjs.com/guides/basics/validation |
| `@adonisjs/redis` | Redis client | https://docs.adonisjs.com/guides/database/redis |
| `@adonisjs/mail` | Email sending | https://docs.adonisjs.com/guides/digging_deeper/mail |
| `@adonisjs/cache` | Caching | https://docs.adonisjs.com/guides/digging_deeper/cache |
| `@adonisjs/bouncer` | Authorization | https://docs.adonisjs.com/guides/auth/authorization |
| `@adonisjs/queue` | Background jobs | https://docs.adonisjs.com/guides/digging_deeper/queues |
| `@adonisjs/drive` | File storage | https://docs.adonisjs.com/guides/digging_deeper/drive |
| `edge` | Template engine | https://docs.adonisjs.com/reference/edge |
| `@adonisjs/vite` | Vite integration | https://docs.adonisjs.com/guides/frontend/vite |
| `@adonisjs/bouncer` | Authorization | https://docs.adonisjs.com/guides/auth/authorization |
| `@adonisjs/redis` | Redis client | https://docs.adonisjs.com/guides/database/redis |
| `@adonisjs/session` | Sessions | https://docs.adonisjs.com/guides/basics/session |

## Core Concepts

### Routing
Routes are defined in `start/routes.ts` using the router service:
```ts
import router from '@adonisjs/core/services/router'

router.get('/posts', [controllers.Posts, 'index'])
router.post('/posts', [controllers.Posts, 'store'])
router.get('/posts/:id', [controllers.Posts, 'show'])
```

Docs: https://docs.adonisjs.com/guides/basics/routing

### Controllers
Controllers organize route handlers into classes:
```ts
import type { HttpContext } from '@adonisjs/core/http'

export default class PostsController {
  async index({ request, response }: HttpContext) {
    return { posts: [] }
  }
}
```

Docs: https://docs.adonisjs.com/guides/basics/controllers

### HTTP Context
The HTTP context provides access to request-specific data:
```ts
router.get('/posts/:id', async ({ params, request, response, auth, logger }) => {
  const id = params.id
  const query = request.qs()
  const user = auth.user
  logger.info('Fetching post')
  return response.json({ id })
})
```

Available properties: `request`, `response`, `params`, `query`, `body`, `auth`, `session`, `logger`, `cookies`, `multipart`

Docs: https://docs.adonisjs.com/guides/basics/http_context

### Models (Lucid ORM)
```ts
import { BaseModel, column } from '@adonisjs/lucid'

export default class Post extends BaseModel {
  @column({ isPrimary: true })
  declare id: number

  @column()
  declare title: string
}
```

Docs: https://docs.adonisjs.com/guides/database/lucid

### Middleware
```ts
import type { HttpContext } from '@adonisjs/core/http'
import type { NextFn } from '@adonisjs/core/types/http'

export default class AuthMiddleware {
  async handle(ctx: HttpContext, next: NextFn) {
    // Check authentication
    await next()
  }
}
```

Docs: https://docs.adonisjs.com/guides/basics/middleware

### File Uploads
```ts
import { multipart } from '@adonisjs/core/bodyparser'

// Handle file upload
async upload({ request, response }: HttpContext) {
  const file = request.file('avatar', {
    size: '2mb',
    extnames: ['jpg', 'png', 'gif']
  })
  
  if (file) {
    await file.move(toAbsolute('./uploads'))
  }
}
```

Docs: https://docs.adonisjs.com/guides/basics/file_uploads

### Body Parser
```ts
// config/bodyparser.ts
export default defineConfig({
  json: { limit: '2mb' },
  form: { limit: '20kb' },
  multipart: { limit: '20mb' }
})
```

Docs: https://docs.adonisjs.com/guides/basics/body_parser

### Static Files
Serve static assets from `public/` directory:
```ts
// Already configured by default
// Access: http://localhost:3000/images/logo.png
```

Docs: https://docs.adonisjs.com/guides/basics/static_file_server

### URL Builder
```ts
import { urlBuilder } from '@adonisjs/core/services/url'

const link = urlBuilder('/posts/:id').params({ id: 1 }).build()
// /posts/1
```

Docs: https://docs.adonisjs.com/guides/basics/url_builder

### Exception Handling
```ts
// Custom exceptions
import { Exception } from '@adonisjs/core'

export default class MyException extends Exception {
  static status = 403
  message = 'Custom error'
}

// Global handler in start/exception.ts
export default class Handler implements ExceptionHandlerInterface {
  handle(error, { response }) {
    response.status(error.status).json({ error: error.message })
  }
}
```

Docs: https://docs.adonisjs.com/guides/basics/exception_handling

### Debugging
```ts
import logger from '@adonisjs/core/services/logger'

logger.info({ user: user.id }, 'Debug info')
// Use VSCode debugger or node --inspect
```

Docs: https://docs.adonisjs.com/guides/basics/debugging

### Event Emitter
```ts
import Event from '@adonisjs/core/services/event'

// Emit event
await Event.emit('user:registered', { user })

// Listen
Event.on('user:registered', async ({ user }) => {
  // Handle event
})
```

Docs: https://docs.adonisjs.com/guides/digging_deeper/emitter

### Application Lifecycle
```ts
// Service provider lifecycle
export default class AppProvider {
  async boot() {}    // Runs after providers are registered
  async start() {}   // Runs during start phase
  async ready() {}  // Runs when app is ready
  async shutdown() {} // Runs on graceful shutdown
}
```

Docs: https://docs.adonisjs.com/guides/concepts/application_lifecycle

### Service Providers
```ts
// app/providers/app_provider.ts
export default class AppProvider {
  register() {
    // Register bindings
    this.app.singleton('my:service', () => new MyService())
    this.app.bind('my:service', () => new MyService())
  }

  async boot() {
    // Initialize after all providers
  }
}
```

Docs: https://docs.adonisjs.com/guides/concepts/service_providers

### Atomic Locks
```ts
import lock from '@adonisjs/lock/services/lock'

// Acquire lock
await lock.acquire('process-payment', 30000, async () => {
  // Only one process can run this at a time
})

// Different acquisition strategies
await lock.safeAcquire()  // Returns null if locked
await lock.stuck()        // Throws if cannot acquire
```

Docs: https://docs.adonisjs.com/guides/digging_deeper/locks

### Health Checks
```ts
import { HealthChecks, DiskSpaceCheck } from '@adonisjs/core/health'

export const healthChecks = new HealthChecks().register([
  new DiskSpaceCheck(),
])

// In controller
async health({ response }) {
  const result = await healthChecks.run()
  return response.json(result)
}
```

Docs: https://docs.adonisjs.com/guides/digging_deeper/health_checks

### Transmit (SSE)
Server-Sent Events for real-time updates:
```ts
import transmit from '@adonisjs/transmit/services/transmit'

// Broadcast to channel
await transmit.emit('posts:new', { post })

// Client side
import { useTransmit } from '@adonisjs/transmit'
const { on } = useTransmit()
on('posts:new', (post) => console.log(post))
```

Docs: https://docs.adonisjs.com/guides/digging_deeper/server_sent_events

### i18n (Internationalization)
```ts
import i18n from '@adonisjs/i18n/services/i18n'

// Translate
t('messages.welcome', { name: 'John' })

// Format
i18n.formatNumber(1000, { style: 'currency', currency: 'USD' })
i18n.formatDate(new Date())
```

Docs: https://docs.adonisjs.com/guides/digging_deeper/i18n

### OpenTelemetry
```ts
// Tracing with OpenTelemetry
// Auto-instrumentation enabled by default
// Manual spans
import { tracer } from '@adonisjs/core/services/otel'

const span = tracer.startSpan('my-operation')
try {
  // operation
} finally {
  span.end()
}
```

Docs: https://docs.adonisjs.com/guides/digging_deeper/opentelemetry

### Container Services
```ts
import { inject } from '@adonisjs/core'

// Bind to container manually
import app from '@adonisjs/core/services/app'
app.bind('my:service', () => new MyService())

// Resolve
const service = app.make('my:service')
```

Docs: https://docs.adonisjs.com/guides/concepts/container_services

### Barrel Files
Use barrel files to simplify imports:
```ts
// app/models/index.ts
export { default as User } from './user.js'
export { default as Post } from './post.js'

// Import cleanly
import { User, Post } from '#models'
```

Docs: https://docs.adonisjs.com/guides/concepts/barrel_files

### Scaffolding
```ts
// Custom assembler hooks
// vite.config.ts
export default defineConfig({
  assembler: {
    preScript: 'console.log("before compile")',
  }
})
```

Docs: https://docs.adonisjs.com/guides/concepts/scaffolding

### Extending AdonisJS
```ts
// Add macros to existing classes
import router from '@adonisjs/core/services/router'

router.macro('myHelper', () => {
  return 'custom behavior'
})
```

Docs: https://docs.adonisjs.com/guides/concepts/extending_adonisjs

### Assembler Hooks
```ts
// Run code during build process
// adonisrc.ts
export default defineConfig({
  hooks: {
    buildStarting: [() => import('./hooks/build')],
    buildCompleted: [() => import('./hooks/build')],
  }
})
```

Docs: https://docs.adonisjs.com/guides/concepts/assembler_hooks

## Security

### Hashing
```ts
import hash from '@adonisjs/core/services/hash'

const hashed = await hash.make(password)
const valid = await hash.verify(password, hashed)
const needsRehash = hash.needsReHash(hashed)
```

Docs: https://docs.adonisjs.com/guides/security/hashing

### Encryption
```ts
import encryption from '@adonisjs/core/services/encryption'

// Encrypt
const encrypted = encryption.encrypt({ data: 'secret' })

// Decrypt
const decrypted = encryption.decrypt(encrypted)

// Message Verifier (sign without encrypt)
const signed = encryption.sign({ data: 'value' })
const verified = encryption.verify(signed)
```

Docs: https://docs.adonisjs.com/guides/security/encryption

### Rate Limiting
```ts
import { rateLimit } from '@adonisjs/core/rate_limiter'

// Route-level
router.get('/api', () => {}).use(rateLimit({
  limit: 100,
  window: 3600
}))

// Global
router.use(rateLimit({ limit: 50, window: 60 }))
```

Docs: https://docs.adonisjs.com/guides/security/rate_limiting

### CORS
```ts
// config/cors.ts
export default defineConfig({
  origin: ['https://example.com'],
  methods: ['GET', 'POST', 'PUT', 'DELETE'],
  headers: ['Content-Type', 'Authorization'],
  exposeHeaders: ['X-Total-Count'],
  credentials: true,
})
```

Docs: https://docs.adonisjs.com/guides/security/cors

### Securing SSR
```ts
// CSRF protection (enabled by default)
// XSS protection (Edge auto-escapes)
// Content Security Policy
// config/security.ts
export default defineConfig({
  csp: {
    directives: {
      defaultSrc: ["'self'"],
    }
  }
})
```

Docs: https://docs.adonisjs.com/guides/security/securing_ssr_applications

### Validation
```ts
import { schema, rules } from '@adonisjs/core/validator'

const createPostSchema = schema.create({
  title: schema.string([rules.minLength(3), rules.maxLength(255)]),
  content: schema.string(),
})
```

Docs: https://docs.adonisjs.com/guides/basics/validation

### Dependency Injection
Use `@inject()` decorator for automatic dependency resolution:
```ts
import { inject } from '@adonisjs/core'

@inject()
export default class PostsController {
  constructor(protected postService: PostService) {}
}
```

Docs: https://docs.adonisjs.com/guides/concepts/dependency_injection

### Authentication
Guards: Session (web apps), Access Tokens (APIs/mobile), Basic Auth

```ts
import type { HttpContext } from '@adonisjs/core/http'

export default class AuthController {
  async login({ auth, request }: HttpContext) {
    const { email, password } = request.only(['email', 'password'])
    const user = await auth.use('session').verifyCredentials(email, password)
    await auth.use('session').login(user)
  }
}
```

Docs: https://docs.adonisjs.com/guides/auth/introduction

### Session Guard
```ts
// Login
await auth.use('session').login(user)

// Logout
await auth.use('session').logout()

// Check authenticated
const user = auth.user

// Remember me
await auth.use('session').login(user, { rememberMe: true })
```

Docs: https://docs.adonisjs.com/guides/auth/session_guard

### Access Tokens Guard
```ts
// Issue token
const token = await user.accessTokens.create({
  name: 'my-device',
  abilities: ['read', 'write'],
  expiresIn: '7 days'
})

// Use token (Authorization header)
await auth.use('api').verify()

// Revoke token
await user.accessTokens.delete(token)
```

Docs: https://docs.adonisjs.com/guides/auth/access_tokens_guard

### Basic Auth Guard
```ts
// Login with basic auth
// Client sends Authorization: Basic base64(email:password)
await auth.use('basic').check()
```

Docs: https://docs.adonisjs.com/guides/auth/basic_auth_guard

### Custom Auth Guard
```ts
// Create custom guard
import { type GuardContract, type ProviderContract } from '@adonisjs/auth'

export class MyGuard implements GuardContract<any, any> {
  constructor(protected provider: ProviderContract) {}
  async authenticate() { /* ... */ }
  async login() { /* ... */ }
}
```

Docs: https://docs.adonisjs.com/guides/auth/custom_auth_guard

### Verifying User Credentials
```ts
const user = await auth.use('session').verifyCredentials(email, password)
if (!user) {
  throw new ApiException('Invalid credentials')
}
```

Docs: https://docs.adonisjs.com/guides/auth/verifying_user_credentials

### Social Authentication (Oauth)
```ts
import { oauth2 } from '@adonisjs/auth'

// Configure OAuth providers in config/auth.ts
// Google, GitHub, etc.

// Login redirect
router.get('/auth/google', async ({ response }) => {
  return response.redirect(oauth2.getRedirectUrl('google'))
})

// Callback
router.get('/auth/google/callback', async ({ oauth2, auth }) => {
  const user = await oauth2.verify('google')
  await auth.use('session').login(user)
})
```

Docs: https://docs.adonisjs.com/guides/auth/social_authentication

### Authorization (Bouncer)
```ts
import { authorize } from '@adonisjs/bouncer'

await authorize('deletePost', post)
```

Docs: https://docs.adonisjs.com/guides/auth/authorization

## Ace CLI Commands

Run commands via `node ace <command>`:
```sh
node ace list                    # List all commands
node ace make:controller Posts   # Create controller
node ace make:model Post         # Create model
node ace make:migration posts    # Create migration
node ace make:validator Post     # Create validator
node ace migration:run           # Run migrations
node ace db:seed                 # Seed database
node ace build                   # Build production app
node ace repl                    # Interactive REPL
```

Docs: https://docs.adonisjs.com/guides/ace/introduction

### Creating Commands
```ts
import { BaseCommand } from '@adonisjs/core/ace'

export default class GreetCommand extends BaseCommand {
  static commandName = 'greet'
  static description = 'Greet a user'
  
  async run() {
    this.logger.info('Hello!')
  }
}
```

Docs: https://docs.adonisjs.com/guides/ace/creating_commands

### Command Arguments
```ts
static arguments = [
  {
    name: 'name',
    type: 'string',
    description: 'User name',
    required: true
  }
]
```

Docs: https://docs.adonisjs.com/guides/ace/args

### Command Flags
```ts
static flags = {
  format: flags.option({ alias: 'f', description: 'Output format' }),
  verbose: flags.boolean({ alias: 'v', description: 'Verbose output' }),
}
```

Docs: https://docs.adonisjs.com/guides/ace/flags

### Interactive Prompts
```ts
import { prompt } from '@adonisjs/core/prompts'

const name = await prompt.text('What is your name?')
const choice = await prompt.choice('Select option', ['a', 'b', 'c'])
const confirmed = await prompt.confirm('Continue?')
```

Docs: https://docs.adonisjs.com/guides/ace/prompts

### TUI (Terminal UI)
```ts
import { table, colors } from '@adonisjs/core/tui'

table(['Name', 'Age'], [['John', '30']])
console.log(colors.green('Success'))
```

Docs: https://docs.adonisjs.com/guides/ace/tui

### REPL
```sh
node ace repl
# Interactive shell with app loaded
```

Docs: https://docs.adonisjs.com/guides/ace/repl

## Migrations

Create and run migrations:
```sh
node ace make:migration posts
node ace migration:run
node ace migration:rollback
```

Docs: https://docs.adonisjs.com/guides/database/lucid#migrations

## Events

Listen to framework events:
```ts
import Event from '@adonisjs/core/services/event'

Event.on('db:query', (query) => {
  console.log(query.sql)
})
```

Docs: https://docs.adonisjs.com/reference/events

## Testing

Test files in `tests/` directory:
```ts
import { test } from '@japa/runner'

test('should create a post', async ({ client }) => {
  const response = await client.post('/posts').form({
    title: 'Hello',
    content: 'World'
  })
  response.assertStatus(201)
})
```

Docs: https://docs.adonisjs.com/guides/testing/introduction

### API Tests
```ts
test('create post', async ({ client }) => {
  const response = await client.post('/posts').form({
    title: 'Hello',
    content: 'World'
  })
  response.assertStatus(201)
})
```

Docs: https://docs.adonisjs.com/guides/testing/api_tests

### Browser Tests
```ts
import { test } from '@japa/runner'

test('homepage loads', async ({ page }) => {
  await page.goto('/')
  await page.assertTitle('Home')
})
```

Docs: https://docs.adonisjs.com/guides/testing/browser_tests

### Console Tests
```ts
test('greet command', async ({ assert, process }) => {
  const { stdout } = await process.run('node ace greet')
  stdout.assertContains('Hello world')
})
```

Docs: https://docs.adonisjs.com/guides/testing/console_tests

### Test Doubles
```ts
import { spy, stub, mock } from '@japa/mock'

spy.on(obj, 'method')        // Track calls
stub(obj, 'method').returns() // Mock return value
mock.route('GET', '/posts').respond({ posts: [] })
```

Docs: https://docs.adonisjs.com/guides/testing/test_doubles

### Resetting State Between Tests
```ts
// Database transactions
await db.transaction(async (trx) => {
  Database.trx = trx
  await test.run()
  Database.trx = null
})

// Using fakes
drive.fake()
cache.fake()
mail.fake()
```

Docs: https://docs.adonisjs.com/guides/testing/resetting_state_between_tests

## Configuration Files

| File | Purpose |
|------|---------|
| `config/app.ts` | App settings, env vars |
| `config/database.ts` | Database connections |
| `config/auth.ts` | Auth guards config |
| `config/session.ts` | Session config |
| `config/logger.ts` | Logging config |
| `config/redis.ts` | Redis config |
| `adonisrc.ts` | Project metadata, commands |

Docs: https://docs.adonisjs.com/reference/adonisrc_file

## Services Reference

Access services via dependency injection or import directly:

| Service | Import | Docs |
|---------|--------|------|
| Router | `@adonisjs/core/services/router` | https://docs.adonisjs.com/guides/basics/routing |
| Response | `@adonisjs/core/services/response` | https://docs.adonisjs.com/guides/basics/response |
| Logger | `@adonisjs/core/services/logger` | https://docs.adonisjs.com/guides/digging_deeper/logger |
| Event | `@adonisjs/core/services/event` | https://docs.adonisjs.com/reference/events |
| Config | `@adonisjs/core/services/config` | https://docs.adonisjs.com/reference/application |
| DB | `@adonisjs/lucid/services/db` | https://docs.adonisjs.com/guides/database/lucid |
| Hash | `@adonisjs/core/services/hash` | https://docs.adonisjs.com/guides/security/hashing |
| Cache | `@adonisjs/cache/services/cache` | https://docs.adonisjs.com/guides/digging_deeper/cache |
| Mail | `@adonisjs/mail/services/mail` | https://docs.adonisjs.com/guides/digging_deeper/mail |
| Drive | `@adonisjs/drive/services/drive` | https://docs.adonisjs.com/guides/digging_deeper/drive |
| Redis | `@adonisjs/redis/services/redis` | https://docs.adonisjs.com/guides/database/redis |

## Background Jobs (Queues)

The `@adonisjs/queue` package handles background job processing:
```ts
import { JobsQueue } from '@adonisjs/queue/services/queue'

export default class SendWelcomeEmail extends JobsQueue {
  static async dispatch(userId: number) {
    const job = await this.queue.create(SendWelcomeEmail, { userId })
    return job
  }

  async handle({ userId }: { userId: number }) {
    // Process job in background
  }
}
```

Docs: https://docs.adonisjs.com/guides/digging_deeper/queues

## Caching

Use the cache service for improved performance:
```ts
import cache from '@adonisjs/cache/services/cache'

// Simple cache
const value = await cache.get('key')
await cache.set('key', 'value', 60) // 60 seconds

// Multi-tier caching (L1 memory + L2 Redis)
const user = await cache
  .use('redis')
  .remember('user:1', 3600, () => fetchUser(1))
```

Docs: https://docs.adonisjs.com/guides/digging_deeper/cache

## File Storage (Drive)

Store files locally or in the cloud:
```ts
import drive from '@adonisjs/drive/services/drive'

// Upload file
await drive.use('s3').put('avatars/user1.png', file.contents)

// Get public URL
const url = await drive.use('s3').getUrl('avatars/user1.png')

// Signed URL (private files)
const signedUrl = await drive.use('s3').getSignedUrl('private/doc.pdf')
```

Docs: https://docs.adonisjs.com/guides/digging_deeper/drive

## Email

Send emails using the mail service:
```ts
import mail from '@adonisjs/mail/services/mail'

await mail.send((message) => {
  message.to(user.email)
  message.from('noreply@example.com')
  message.subject('Welcome')
  message.htmlView('emails/welcome', { user })
})
```

Docs: https://docs.adonisjs.com/guides/digging_deeper/mail

## Frontend Integration

### Vite
```ts
import { vite } from '@adonisjs/vite/services/vite'

// In Edge templates
{{ vite.asset('resources/js/app.js') }}
```

Docs: https://docs.adonisjs.com/guides/frontend/vite

### Edge Templates
```edge
@layout()
  @each(post in posts)
    <h1>{{ post.title }}</h1>
  @end

@if(auth.isAuthenticated)
  <p>Welcome, {{ auth.user.name }}</p>
@end
```

Docs: https://docs.adonisjs.com/guides/frontend/edgejs

### Inertia
```tsx
import { Inertia } from '@adonisjs/inertia'

// Visit
Inertia.visit('/posts', { data: { search: 'foo' } })

// Form
import { Form } from '@adonisjs/inertia/react'
<Form route="posts.store" data={{ title: '' }} />
```

Docs: https://docs.adonisjs.com/guides/frontend/inertia

### TanStack Query
```tsx
import { useQuery, useMutation } from '@tanstack/react-query'

// Fetch
const { data } = useQuery({
  queryKey: ['posts'],
  queryFn: () => client.get('/api/posts')
})

// Mutate
const mutation = useMutation({
  mutationFn: (newPost) => client.post('/api/posts', newPost)
})
```

Docs: https://docs.adonisjs.com/guides/frontend/tanstack_query

### API Client
```ts
import { apiClient } from '@adonisjs/core/services/api_client'

const response = await apiClient.get('/posts')
const data = response.json()
```

Docs: https://docs.adonisjs.com/guides/frontend/api_client

### Transformers
```ts
import transformer from '@adonisjs/transformers/services/transformer'

// Transform API responses
const transformed = await transformer.serialize(post, {
  include: ['author', 'comments'],
  fields: ['id', 'title']
})
```

Docs: https://docs.adonisjs.com/guides/frontend/transformers

## Service Providers

Register application services and bindings:
```ts
// app/providers/app_provider.ts
export default class AppProvider {
  register() {
    this.app.singleton('my:service', () => new MyService())
  }

  async boot() {
    // Initialize after all providers
  }
}
```

Docs: https://docs.adonisjs.com/guides/concepts/service_providers

```ts
import { typedResolve, typedValues } from '@adonisjs/core/helpers'

typedResolve<Model>() // Type-safe class resolver
typedValues({ a: 1, b: 2 }) // Type-safe object values
```

Docs: https://docs.adonisjs.com/reference/types_helpers

### String Helpers
```ts
import string from '@adonisjs/core/helpers/string'

string.excerpt(html, 70)              // Truncate with ellipsis
string.capitalize('hello world')       // Hello World
string.pluralize('post', 2)            // posts
string.snakeCase('helloWorld')        // hello_world
string.camelCase('hello_world')       // helloWorld
string.slug('Hello World')            // hello-world
string.truncate('long text', 20)      // Truncate with limit
```

Docs: https://docs.adonisjs.com/reference/string_helpers

### Helpers Module
```ts
import is from '@adonisjs/core/helpers/is'

is.object(value)           // Check if object
is.array(value)           // Check if array
is.string(value)          // Check if string
is.number(value)          // Check if number
is.boolean(value)         // Check if boolean
is.date(value)            // Check if Date
is.blank(value)          // Check if null/undefined/empty
```

Docs: https://docs.adonisjs.com/reference/helpers

### Edge Template Reference
```edge
@layout('main')
  @set('title', 'Page Title')

@each(items as item)
  {{ item.name }}
@end

@if(condition)
  Show this
@else
  Show that
@end

@include('partials/header')
@component('card', { title: 'Hello' })
@slot('body')
  Content
@end
```

Docs: https://docs.adonisjs.com/reference/edge

### Exception Reference
```ts
import { errors } from '@adonisjs/core/exceptions'

throw new errors.E_ROUTE_NOT_FOUND(route)
throw new errors.E_VALIDATION_ERROR({ messages })
```

Docs: https://docs.adonisjs.com/reference/exceptions

### Commands Reference
```sh
node ace make:controller User
node ace make:model User
node ace make:migration create_users_table
node ace make:validator CreateUser
node ace make:middleware Auth
node ace make:service UserService
node ace make:policy UserPolicy
node ace migration:run
node ace migration:rollback
node ace db:seed
node ace db:seed --files="users"
node ace build
node ace repl
node ace list
```

Docs: https://docs.adonisjs.com/reference/commands

### adonisrc.ts Reference
```ts
export default defineConfig({
  metaFile: true,
  directories: {
    app: 'app',
    config: 'config',
    contracts: 'contracts',
  },
  commands: [() => import('./commands')],
  providers: [() => import('@adonisjs/core/providers/app_provider')],
  preloads: [() => import('./start/routes')],
  tests: {
    suites: [{ name: 'functional', files: ['tests/**/*.spec.ts'] }]
  }
})
```

Docs: https://docs.adonisjs.com/reference/adonisrc_file

### Config Reference

**config/app.ts**
```ts
export default defineConfig({
  appName: 'MyApp',
  appVersion: '1.0.0',
  http: { cookieMaxAge: 3600000 },
  logger: { default: 'console' }
})
```

Docs: https://docs.adonisjs.com/reference/config/app.md

**config/bodyparser.ts**
```ts
export default defineConfig({
  json: { limit: '2mb' },
  form: { limit: '20kb' },
  multipart: { limit: '20mb' }
})
```

Docs: https://docs.adonisjs.com/reference/config/bodyparser.md

### Configuration & Environment
Three config systems:
1. **Config files** - `config/*.ts` for app settings (DB, mail, sessions)
2. **Environment variables** - `.env` files with type-safe validation
3. **adonisrc.ts** - Framework configuration (providers, commands, preload)

```ts
import env from '#start/env'

// Type-safe env access
const dbHost = env.get('DB_HOST')
const port = env.get('PORT', 3000) // with default
```

Environment-specific configs: `.env`, `.env.development`, `.env.test`, `.env.production`

Docs: https://docs.adonisjs.com/start/configuration

## Best Practices

1. **Use controllers** - Keep route handlers organized in controller classes
2. **Use services** - Extract business logic into service classes
3. **Use validation** - Always validate input with the validator package
4. **Use migrations** - Never modify database schema directly
5. **Use type safety** - Leverage TypeScript throughout
6. **Use dependency injection** - Let the IoC container manage dependencies
7. **Use environment variables** - Store secrets in `.env` files
8. **Use queues for heavy tasks** - Offload email, processing to background jobs
9. **Use cache wisely** - Cache expensive computations but invalidate properly

## Migration from v5/v6

Key changes in v7:
- ESM-only modules
- No more `app.start` files - use `start/kernel.ts` and `start/routes.ts`
- Services imported directly rather than from `Contracts`
- Updated authentication system with guards/providers
- Vite for frontend bundling instead of Webpack

Docs: https://docs.adonisjs.com/start/resources/upgrade_guide

## Starter Kits

| Kit | Use Case |
|-----|----------|
| `web` | Full-stack with Edge templates |
| `inertia` | Full-stack with Inertia + React/Vue |
| `api` | API-only with separate frontend (Turborepo) |

Create new project: `node ace init my-app --kit=web`

Docs: https://docs.adonisjs.com/start/installation

## Pick Your Path

AdonisJS offers three frontend approaches:

### Hypermedia
- Server-rendered HTML with Edge templates
- Minimal JavaScript, uses Alpine.js or HTMX
- Best for: content sites, simple web apps

### Inertia
- Server-rendered with Inertia (React/Vue)
- Full JS framework on client
- Best for: complex SPAs, modern teams

### API-only
- JSON API backend with separate frontend
- Turborepo monorepo structure
- Best for: mobile apps, SPAs, microservices

Docs: https://docs.adonisjs.com/start/pick_your_path

## Additional Resources

### Contributing
```ts
// Contributing to AdonisJS
// See CONTRIBUTING.md for guidelines
```

Docs: https://docs.adonisjs.com/start/resources/contributing

### Governance
- Open source project with clear structure
- Core team maintains official packages

Docs: https://docs.adonisjs.com/start/resources/governance

### FAQs
Common questions about AdonisJS:
- Migration paths, performance, deployment, etc.

Docs: https://docs.adonisjs.com/start/faqs

### Deployment
```sh
# Production build
npm run build

# Start production
node bin/server.js

# Or with Ace
node ace serve --production
```

Docs: https://docs.adonisjs.com/start/deployment

### Dev Environment
- Hot reload enabled by default
- Vite for frontend, ts-node for backend

Docs: https://docs.adonisjs.com/start/dev_environment

### Tutorial: Hypermedia (Full-Stack with Edge)
Step-by-step building DevShow app:
- overview - Introduction to DevShow project
- routes_controllers_and_views - Routes and controllers setup
- database_and_models - Lucid models and migrations
- forms_and_validation - Form handling and validation
- authorization - Authentication and authorization
- cli_and_repl - Using Ace CLI and REPL
- styling_and_cleanup - Final styling and cleanup
- deployment - Deploy to production

Docs: https://docs.adonisjs.com/start/tutorial/hypermedia/overview

### Tutorial: React (Full-Stack with Inertia)
Step-by-step building DevShow app with React:
- overview - Introduction to DevShow project
- routes_controllers_and_views - Routes and controllers with Inertia
- database_and_models - Lucid models and migrations
- forms_and_validation - Form handling and validation
- authorization - Authentication and authorization
- cli_and_repl - Using Ace CLI and REPL
- styling_and_cleanup - Final styling and cleanup
- deployment - Deploy to production

Docs: https://docs.adonisjs.com/start/tutorial/react/overview

### Folder Structure
```sh
# Standard structure
app/controllers, models, services, middleware, validators
config/          # Config files
database/migrations, seeders, factories
start/           # routes.ts, kernel.ts, env.ts
tests/           # Test suites

# API kit (monorepo with Turborepo)
apps/backend/    # AdonisJS API
apps/frontend/   # Separate frontend
```

Docs: https://docs.adonisjs.com/start/folder_structure

### Releases
- Version history and changelogs
- Release notes for each version

Docs: https://docs.adonisjs.com/start/resources/releases