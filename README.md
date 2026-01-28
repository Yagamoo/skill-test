# Laravel Skill Test

## 1. Overview

Implement RESTful routes for a `Post` model using Laravel 12. Posts support **drafts**, **scheduled publishing**, and **authenticated user operations**.

## 2. Workflow

1. Clone this repository and set up the local environment.
2. Change the remote repository to your own public repository (do **not** delete commit history)
3. Implement the required features described below.
4. Push all changes to your public repository and let us know the repository URL.

## 3. Specifications

### General

- Follow Laravel 12 best practices and official documentation (https://laravel.com/docs/12.x)
- Write clear, meaningful commit messages with reasonable commit sizes
- View files are **not required**

### Post Status

- The `posts` table already exists.
- You are expected to understand how to determine whether a post is a draft, scheduled, or published by carefully examining the table structure, seed data, and business requirements.
- Scheduled posts do not require a cron job. They will be published automatically when the publish date comes.

### Authentication

- Use Laravel’s built-in **session & cookie-based authentication**
- Token-based systems (Sanctum, Passport, etc.) are not required

## 4. Requirements

### 4-1. `posts.index`

- Retrieve a paginated list of active posts (20 per page)
- Include the user (author) data for each post
- Exclude draft and scheduled posts
- Return a JSON response in a format suitable for passing to views

### 4-2. `posts.create`

- Only authenticated users can access this route
- Return the string `posts.create`

### 4-3. `posts.store`

- Only authenticated users can create new posts
- Validate submitted data before creating the post
- Return an appropriate response for a `POST` request

### 4-4. `posts.show`

- Retrieve a single active post
- Return a JSON response in a format suitable for passing to views
- Return **404** if the post is a draft or scheduled

### 4-5. `posts.edit`

- Only the post author can access this route
- Return the string `posts.edit`

### 4-6. `posts.update`

- Only the post author can update the post
- Validate submitted data before updating the post
- Return an appropriate response for a `PUT/PATCH` request

### 4-7. `posts.destroy`

- Only the post author can delete the post
- Return an appropriate response for a `DELETE` request

## Recommended Environment

- PHP 8.4
- Node v22.15.0
- Database: SQLite
- Server: Laravel built-in server

## Database Seeding

Sample users and posts are provided.

```bash
php artisan db:seed
```
# How to Test
Since this project focuses on the API/Backend logic and does not include view files, you can test the endpoints using **Postman**, **Insomnia**, or **cURL**.

## Requirements & Endpoints
| Method | Endpoint | Access | Description |
| :--- | :--- | :--- | :--- |
| **GET** | `/posts` | Public | Paginated list of active posts (20 per page). Includes author data. |
| **GET** | `/posts/{id}` | Public | Show single active post. Returns **404** if the post is draft/scheduled. |
| **GET** | `/posts/create` | Authenticated | Returns string `posts.create`. |
| **POST** | `/posts` | Authenticated | Validate and store a new post linked to the auth user. |
| **GET** | `/posts/{id}/edit` | Author Only | Returns string `posts.edit`. |
| **PUT** | `/posts/{id}` | Author Only | Validate and update the specified post. |
| **DELETE** | `/posts/{id}` | Author Only | Permanently delete the specified post. |

## Quick Start for API Testing
1. Login First: Send a POST request to /login with email and password from the seeder to establish a session.
2. Postman Cookies: Postman will automatically store the session cookie for subsequent authenticated requests.
3. CSRF: For testing purposes, CSRF protection is disabled for /login and posts/* routes in bootstrap/app.php.
4. Status Filter: "Active" posts are defined as is_draft: false AND published_at <= now().