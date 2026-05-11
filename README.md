# Photo Gallery

A small Rails + Hotwire photo gallery application demonstrating server-rendered interactivity with Turbo Frames, Stimulus, and Tailwind CSS.

Users can authenticate, browse seeded photos, and like or unlike photos without full page reloads.

## Tech Stack

* Ruby 4.0.3
* Rails 8.1.3
* SQLite3
* Devise
* Turbo
* Stimulus
* Tailwind CSS
* RSpec

## Setup

Install dependencies and prepare the database:

```sh
bundle install
bin/rails db:prepare
bin/rails db:seed
```

## Demo Credentials

```text
Email: demo@example.com
Password: password123
```

The demo user and seeded photo data are created from `db/seeds.rb`. Photo records are imported from `db/photos.csv` and persisted in the database rather than read at runtime.

## Running the Application

```sh
bin/dev
```

Then visit:

```text
http://localhost:3000
```

## Running the Test Suite

```sh
bundle exec rspec
```

The test suite includes coverage for:

* Authentication redirect behavior
* Duplicate-like prevention
* Like/unlike interaction flow

## Implementation Notes

### Authentication

Authentication is implemented with Devise using a seeded demo user, since self-service registration was not required for the challenge.

### Photo Importing

Photo data is imported from `db/photos.csv` during seeding and persisted in the database to avoid runtime CSV parsing.

### Likes

Likes are modeled as a join table between users and photos.

A unique composite database index on `[user_id, photo_id]` ensures a user can only like a photo once while maintaining database-level integrity.

### Hotwire Interactivity

The like/unlike UI is isolated within a Turbo Frame so only the relevant portion of the page updates after interaction.

Turbo handles server-driven UI replacement, while a lightweight Stimulus controller provides immediate visual feedback during interactions.

### Testing

The application includes focused RSpec coverage for core business rules and user flows rather than exhaustive framework-level testing.

