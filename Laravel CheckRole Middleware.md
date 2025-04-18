
## 📄 Laravel 11+ — checkRole Middleware Setup & Usage

---

## ✅ 1. Add `role` Field to Users Table

In your migration (`database/migrations/..._create_users_table.php`):

```php
$table->string('role')->default('user'); // Add this
```

Run:

```bash
php artisan migrate
```

---

## 🧱 2. Update `User` Model

In `app/Models/User.php`:

```php
protected $fillable = [
    'name', 'email', 'password', 'role',
];
```

---

## 🛠️ 3. Create `CheckRole` Middleware

```bash
php artisan make:middleware CheckRole
```

Then in `app/Http/Middleware/CheckRole.php`:

```php
namespace App\Http\Middleware;

use Closure;
use Illuminate\Http\Request;
use Symfony\Component\HttpFoundation\Response;

class CheckRole
{
    public function handle(Request $request, Closure $next, ...$roles): Response
    {
        if (!in_array($request->user()?->role, $roles)) {
            abort(403, 'Unauthorized access');
        }

        return $next($request);
    }
}
```

---

## 🧩 4. Register Middleware in Laravel 11 (No Kernel)

In **Laravel 11**, you register middleware in `bootstrap/app.php`.

Find this part in `bootstrap/app.php`:

```php
->withMiddleware(function (Middleware $middleware) {
    //
});
```

Update it like this:

```php
use App\Http\Middleware\CheckRole;

->withMiddleware(function (Middleware $middleware) {
    $middleware->alias([
        'checkRole' => CheckRole::class,
    ]);
});
```

✅ Now, `checkRole` is registered and ready to use.

---

## 🧭 5. Define Role-Based Routes

In `routes/web.php`:

```php
use Illuminate\Support\Facades\Route;
use App\Http\Controllers\AdminController;
use App\Http\Controllers\UserController;

// Admin-only
Route::middleware(['auth', 'checkRole:admin'])->group(function () {
    Route::get('/admin/dashboard', [AdminController::class, 'index']);
});

// User-only
Route::middleware(['auth', 'checkRole:user'])->group(function () {
    Route::get('/user/dashboard', [UserController::class, 'index']);
});

// Shared (admin & user)
Route::middleware(['auth', 'checkRole:admin,user'])->group(function () {
    Route::get('/shared/dashboard', function () {
        return view('dashboard');
    });
});
```

---

## 🧪 6. Seeder (Optional)

In `DatabaseSeeder.php`:

```php
User::create([
    'name' => 'Admin',
    'email' => 'admin@example.com',
    'password' => bcrypt('password'),
    'role' => 'admin',
]);

User::create([
    'name' => 'User',
    'email' => 'user@example.com',
    'password' => bcrypt('password'),
    'role' => 'user',
]);
```

---

## 📘 Summary: File Breakdown

| File                        | Purpose                                |
|-----------------------------|----------------------------------------|
| `users` migration           | Add `role` field                       |
| `User.php`                  | Add `role` to `$fillable`              |
| `CheckRole.php`             | Define role-checking logic             |
| `bootstrap/app.php`         | Register middleware via alias          |
| `routes/web.php`            | Apply role-based route protection      |

---

