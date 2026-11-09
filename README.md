# SupabasePHP

A modern, modular and strongly typed Supabase SDK for PHP.

SupabasePHP is an independent PHP SDK designed to provide a clean, consistent and developer-friendly interface for interacting with Supabase services.

Built for PHP 8.4+, the project follows a modular architecture in which each Supabase service is maintained as an independent Composer package.

## Features

- Modular Composer package architecture.
- Native cURL HTTP transport.
- Authentication and session management.
- PostgreSQL database operations through PostgREST.
- Fluent database query builder.
- File uploads and downloads.
- Realtime subscriptions through WebSockets.
- Supabase Edge Functions.
- Vector search and pgvector integration.
- PSR interoperability.
- Strict typing and PHPDoc support.
- Unit and integration testing.
- Static analysis with PHPStan.

## Requirements

- PHP 8.4 or higher.
- Composer 2.x.
- PHP cURL extension.
- PHP JSON extension.
- OpenSSL extension for supported secure transports.

Additional requirements may apply to individual packages.

Packages

Package| Description
"supabasephp/client"| Main SDK and service integration
"supabasephp/core"| Shared contracts and utilities
"supabasephp/http"| HTTP transport and PSR interoperability
"supabasephp/auth"| Authentication and session management
"supabasephp/database"| PostgREST database client
"supabasephp/storage"| File and bucket management
"supabasephp/realtime"| WebSocket subscriptions
"supabasephp/functions"| Edge Functions
"supabasephp/vector"| Vector search and pgvector integration

Each package can be installed independently when its dependencies are satisfied.

Installation

Install the complete SDK:

composer require supabasephp/client

Install an individual service:

composer require supabasephp/auth

composer require supabasephp/database

## Quick Start
```php
<?php

declare(strict_types=1);

use Supabase\Client;

$client = new Client([
    'url' => $_ENV['SUPABASE_URL'],
    'key' => $_ENV['SUPABASE_KEY'],
]);
```
### Authentication

$session = $client->auth()->signInWithPassword([
    'email' => 'user@example.com',
    'password' => 'your-password',
]);

### Database

$users = $client
    ->from('users')
    ->select('id, name, email')
    ->where('status', '=', 'active')
    ->order('created_at', 'desc')
    ->limit(20)
    ->get();

### Storage

$storage = $client->storage();

$storage
    ->from('avatars')
    ->upload('profile.png', $file);

### Edge Functions

$response = $client->functions()->invoke(
    'hello-world',
    [
        'body' => [
            'name' => 'Developer',
        ],
    ]
);

«The examples describe the intended public API. Refer to the individual package documentation for implemented methods and supported options.»

## Monorepo Structure
```bash
supabasephp/
│
├── packages/
│   ├── client/
│   ├── core/
│   ├── http/
│   ├── auth/
│   ├── database/
│   ├── storage/
│   ├── realtime/
│   ├── functions/
│   └── vector/
│
├── tests/
│   ├── Unit/
│   └── Integration/
│
├── .github/
│   └── workflows/
│
├── composer.json
├── phpunit.xml.dist
├── phpstan.neon
├── pint.json
├── rector.php
├── CONTRIBUTING.md
├── CODE_OF_CONDUCT.md
├── SECURITY.md
└── LICENSE
```
Development

Clone the repository:

git clone https://github.com/YOUR_USERNAME/supabasephp.git

cd supabasephp

Install dependencies:

composer install

Validate Composer configuration:

composer validate --strict

Quality Assurance

Run the test suite:

composer test

Run static analysis:

composer analyse

Format source code:

composer format

Check formatting without modifying files:

composer format:test

Run Rector:

composer refactor

Run all quality checks:
```sh
composer quality
```

## Development Principles

SupabasePHP follows these principles:

- Modularity: Each service has its own independently maintained package.
- Type safety: Strong native types and comprehensive PHPDoc annotations.
- Interoperability: Follow established PHP standards wherever practical.
- Security: Secure defaults, TLS verification and careful credential handling.
- Maintainability: Clear separation of concerns and testable components.
- Performance: Lightweight dependencies and efficient HTTP communication.

## Security

Never expose Supabase secret or service-role credentials in frontend applications.

Keep sensitive credentials in server-side environment variables.

For security vulnerabilities, please follow the instructions in "SECURITY.md" (SECURITY.md).

## Contributing

Contributions are welcome.

Before submitting a pull request:

1. Follow the project's coding standards.
2. Add or update relevant tests.
3. Run PHPStan.
4. Run PHPUnit.
5. Run Laravel Pint.
6. Document significant changes.

Read "CONTRIBUTING.md" (CONTRIBUTING.md) before contributing.

## License

SupabasePHP is open-source software licensed under the MIT License.

See "LICENSE" (LICENSE) for details.
