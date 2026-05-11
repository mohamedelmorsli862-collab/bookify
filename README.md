# Bookify Backend

Laravel backend for the Bookify multi-service reservation platform described in the provided PDFs. The frontend/design layer is intentionally minimal and untouched; this project exposes the API, data model, booking logic, multilingual catalog, and PDF/document structure.

## Stack

- Laravel 12 / PHP 8.2
- MySQL or MariaDB via XAMPP
- REST API under `/api/v1`
- Multilingual API data: French, English, Arabic
- PDF endpoints for project report and booking confirmations

## Local Setup

```bash
composer install
php artisan key:generate
```

Create a MySQL/MariaDB database named `bookify`, then run:

```bash
php artisan migrate:fresh --seed
php artisan serve
```

The API will be available at `http://127.0.0.1:8000/api/v1`.

## Demo Accounts

All seeded accounts use the password `password`.

- Admin: `admin@bookify.test`
- Provider: `provider@bookify.test`
- Client: `client@bookify.test`

## Main API Areas

- Auth: `POST /auth/register`, `POST /auth/login`, `POST /auth/logout`, `POST /auth/forgot-password`, `POST /auth/reset-password`
- Catalog: `GET /domains`, `GET /providers`, `GET /providers/{provider}`, `GET /providers/{provider}/services`
- Availability: `GET /providers/{provider}/availability`, `POST /providers/{provider}/availability/check`
- Bookings: `GET /bookings`, `POST /bookings`, `GET /bookings/{booking}`, `PATCH /bookings/{booking}/cancel`, `PATCH /bookings/{booking}/status`
- Provider workspace: `/provider/dashboard`, `/provider/profile`, `/provider/services`, `/provider/availability-rules`, `/provider/blocked-periods`, `/provider/weekly-schedule`
- Admin workspace: `/admin/dashboard`, `/admin/users`, `/admin/providers/{provider}`, `/admin/domains`
- Documents: `GET /documents/structures`, `GET /documents/project-report.pdf`, `GET /bookings/{booking}/confirmation.pdf`

Protected routes use:

```http
Authorization: Bearer YOUR_TOKEN
```

## Dynamic Reservation Forms

The seeded domains include dynamic schemas for:

- Hotel
- Hair salon
- Gym
- Restaurant
- Spa
- Clinic
- Training center
- Garage
- Photographer

Use `GET /api/v1/domains?lang=fr`, `?lang=en`, or `?lang=ar` to retrieve localized labels and required fields.

## Verification

```bash
php artisan route:list --path=api
php artisan test
```

If `php artisan test` cannot run, finish Composer dev dependencies first with `composer install`.
