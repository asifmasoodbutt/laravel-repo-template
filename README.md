# Laravel Repository Pattern Boilerplate

A clean, scalable, and production-ready Laravel starter template built using the **Repository Design Pattern + Service Layer Architecture**. This boilerplate is designed for reuse across multiple projects with a consistent and maintainable structure.

---

## 🚀 Features

- Fully implemented Repository Design Pattern
- Service Layer for business logic separation
- Thin Controllers (no business logic in controllers)
- RESTful API structure
- Laravel Breeze Authentication
- Role-based access structure (extensible)
- Form Request validation
- API Resource transformation layer
- PSR-compliant clean architecture
- Scalable and modular structure

---

## 🧠 Architecture
Controller → Service → Repository → Model → Database

---

## 📁 Folder Structure
```
app/
│
├── Interfaces/
│ └── Repositories/
│
├── Repositories/
│
├── Services/
│
├── Http/
│ ├── Controllers/
│ │ └── API/
│ │
│ ├── Requests/
│ │
│ ├── Resources/
│
├── Models/
│
├── Providers/
│ └── RepositoryServiceProvider.php
│
├── Traits/
```

---

## ⚙️ Installation

### 1. Clone Project

```
git clone https://github.com/your-username/laravel-repo-boilerplate.git
cd laravel-repo-boilerplate
```

### 2. Install Dependencies

```
composer install
npm install && npm run dev
```

### 3. Setup Environment

```
cp .env.example .env
php artisan key:generate
```

Update .env database settings:

```
DB_DATABASE=your_db
DB_USERNAME=root
DB_PASSWORD=
```
### 4. Run Migrations
```
php artisan migrate
```

### 5. Start Server
```
php artisan serve
```

## 🔐 Authentication

Built using Laravel Breeze:

Login
Register
Logout
Forgot Password
Reset Password

Optional upgrade:

Laravel Sanctum for API authentication

## 🧩 Example CRUD Flow
Controller → Service → Repository → Model

## 🧱 Repository Pattern Example
### Interface

```
interface UserRepositoryInterface
{
    public function all();
    public function find($id);
    public function create(array $data);
}
```

### Repository

```
class UserRepository implements UserRepositoryInterface
{
    public function all()
    {
        return User::all();
    }

    public function find($id)
    {
        return User::findOrFail($id);
    }

    public function create(array $data)
    {
        return User::create($data);
    }
}
```

### Service Layer

```
class UserService
{
    public function __construct(
        protected UserRepositoryInterface $userRepo
    ) {}

    public function getAllUsers()
    {
        return $this->userRepo->all();
    }

    public function createUser(array $data)
    {
        return $this->userRepo->create($data);
    }
}
```

### Controller Example

```
class UserController extends Controller
{
    public function __construct(
        protected UserService $userService
    ) {}

    public function index()
    {
        return response()->json(
            $this->userService->getAllUsers()
        );
    }
}
```

### Repository Binding

```
$this->app->bind(
    UserRepositoryInterface::class,
    UserRepository::class
);
```
Located in:

```
app/Providers/RepositoryServiceProvider.php
```

## 📈 Scalability Improvements
- Modular Architecture (Modules/)
- Multi-tenancy support (stancl/tenancy)
- Event-driven architecture
- Queue-based processing
- Microservices-ready structure

## 🧼 Coding Standards
- PSR-4 compliant
- SOLID principles
- Clean architecture
- No logic in controllers

## 📌 Future Enhancements
- Docker support
- CI/CD pipeline (GitHub Actions)
- Swagger API documentation
- Admin panel (Filament / Nova)
- Redis caching layer

## 🤝 License

MIT License – free to use for personal and commercial projects.

## ⭐ Purpose

This boilerplate is designed to:

- Reduce setup time for new Laravel projects
- Enforce clean architecture
- Ensure scalability from day one
- Standardize backend development structure
