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

### Packages

|Package| Description|
|"supabasephp/client"| Main SDK and service integration|
|"supabasephp/core"| Shared contracts and utilities|
|"supabasephp/http"| HTTP transport and PSR interoperability|
|"supabasephp/auth"| Authentication and session management|
|"supabasephp/database"| PostgREST database client|
|"supabasephp/storage"| File and bucket management|
| "supabasephp/realtime"| WebSocket subscriptions |
|"supabasephp/functions"| Edge Functions|
|"supabasephp/vector"| Vector search and pgvector integration|

Each package can be installed independently when its dependencies are satisfied.

### Installation

Install the complete SDK:

```sh
composer require supabasephp/client
```

Install an individual service:

```sh
composer require supabasephp/database

composer require supabasephp/auth
```

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

```php
$session = $client->auth()->signInWithPassword([
    'email' => 'user@example.com',
    'password' => 'your-password',
]);
```

### Database

```php
$users = $client
    ->from('users')
    ->select('id, name, email')
    ->where('status', '=', 'active')
    ->order('created_at', 'desc')
    ->limit(20)
    ->get();
```

### Storage

```php
$storage = $client->storage();

$storage
    ->from('avatars')
    ->upload('profile.png', $file);
```

### Edge Functions

```php
$response = $client->functions()->invoke(
    'hello-world',
    [
        'body' => [
            'name' => 'Developer',
        ],
    ]
);
```

## Security

Never expose Supabase secret or service-role credentials in frontend applications.

Keep sensitive credentials in server-side environment variables.

For security vulnerabilities, please follow the instructions in ["SECURITY.md"](SECURITY.md).

## Contributing

Contributions are welcome.

Before submitting a pull request:

1. Follow the project's coding standards.
2. Add or update relevant tests.
3. Run PHPStan.
4. Run PHPUnit.
5. Run Laravel Pint.
6. Document significant changes.

Read [CONTRIBUTING.md](CONTRIBUTING.md) before contributing.

## License

SupabasePHP is open-source software licensed under the MIT License.

See ["LICENSE"](LICENSE) for details.
