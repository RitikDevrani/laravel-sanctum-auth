Laravel Sanctum Authentication
🚀 Features

User Registration (with token generation)

User Login (with token generation)

Fetch Authenticated User Details (Protected route)

User Logout (Token revoke)

⚙️ Installation & Setup

1. Clone the Repository

git clone <your-repo-url>
cd project-name


2. Install Dependencies

composer install


3. Environment Setup

cp .env.example .env
php artisan key:generate


Update .env with your database credentials.

4. Run Migrations

php artisan migrate


5. Install Sanctum

composer require laravel/sanctum
php artisan vendor:publish --provider="Laravel\Sanctum\SanctumServiceProvider"
php artisan migrate


6. Middleware Update
In app/Http/Kernel.php, add:

\Laravel\Sanctum\Http\Middleware\EnsureFrontendRequestsAreStateful::class,


inside the api middleware group (if not already added).

7. Run the Server

php artisan serve

📌 API Endpoints
🔹 Public Routes

POST /api/register → Register new user

POST /api/login → Login user

🔹 Protected Routes (Require Token)

GET /api/user → Get authenticated user details

POST /api/logout → Logout user

🧑‍💻 API Testing with Postman
1️⃣ Register User

Endpoint: POST /api/register

Body → raw (JSON):

{
  "name": "Ritik",
  "email": "ritik@example.com",
  "password": "password",
  "password_confirmation": "password"
}


Response:

{
  "user": {
    "id": 1,
    "name": "Ritik",
    "email": "ritik@example.com"
  },
  "token": "1|your_generated_token_here"
}

2️⃣ Login User

Endpoint: POST /api/login

Body → raw (JSON):

{
  "email": "ritik@example.com",
  "password": "password"
}


Response:

{
  "user": {
    "id": 1,
    "name": "Ritik",
    "email": "ritik@example.com"
  },
  "token": "1|new_generated_token_here"
}

3️⃣ Get Authenticated User (Protected Route)

Endpoint: GET /api/user

Headers → Authorization:

Authorization: Bearer <your_token>


Response:

{
  "id": 1,
  "name": "Ritik",
  "email": "ritik@example.com",
  "created_at": "...",
  "updated_at": "..."
}

4️⃣ Logout User

Endpoint: POST /api/logout

Headers → Authorization:

Authorization: Bearer <your_token>


Response:

{
  "message": "Logged out successfully"
}
