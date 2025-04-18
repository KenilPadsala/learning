## 🔹 Relationships Covered:
- **One to One** → `User` ↔ `Profile`
- **One to Many** → `User` → `Post`
- **Many to One** → `Post` → `User` (reverse of One to Many)

---

## 🔁 1. ONE TO ONE – User & Profile

### ✅ CREATE

Create a user and a profile for that user:

```php
$user = User::create([
    'name' => 'John Doe',
    'email' => 'john@example.com',
    'password' => bcrypt('secret'),
]);

$user->profile()->create([
    'bio' => 'I am a web developer.',
    'location' => 'New York',
]);
```

### 👀 READ

Get user with profile:

```php
$user = User::with('profile')->find(1);
echo $user->profile->bio;
```

### 🔄 UPDATE

Update profile:

```php
$user = User::find(1);
$user->profile->update([
    'location' => 'San Francisco',
]);
```

### ❌ DELETE

Delete user and profile:

```php
$user = User::find(1);
$user->profile()->delete();
$user->delete();
```

---

## 🔁 2. ONE TO MANY – User & Posts

### ✅ CREATE

Create a user and multiple posts:

```php
$user = User::create([
    'name' => 'Alice',
    'email' => 'alice@example.com',
    'password' => bcrypt('secret'),
]);

$user->posts()->createMany([
    ['title' => 'First Post', 'body' => 'This is the first post'],
    ['title' => 'Second Post', 'body' => 'Another one'],
]);
```

### 👀 READ

Get user with posts:

```php
$user = User::with('posts')->find(1);
foreach ($user->posts as $post) {
    echo $post->title;
}
```

### 🔄 UPDATE

Update a specific post:

```php
$post = Post::find(1);
$post->update([
    'title' => 'Updated Title',
]);
```

### ❌ DELETE

Delete a post:

```php
$user = User::find(1);
$user->posts()->where('id', 1)->delete();
```

---

## 🔁 3. MANY TO ONE – Post & User (Reverse)

### ✅ CREATE

Create a post and assign to a user:

```php
$user = User::find(1);

$post = new Post([
    'title' => 'New Blog',
    'body' => 'This is a blog post',
]);

$user->posts()->save($post);
// OR
$post->user()->associate($user);
$post->save();
```

### 👀 READ

Get post with author (user):

```php
$post = Post::with('user')->find(1);
echo $post->user->name;
```

### 🔄 UPDATE

Change post's author:

```php
$post = Post::find(1);
$newUser = User::find(2);

$post->user()->associate($newUser);
$post->save();
```

### ❌ DELETE

Delete a post (user stays):

```php
$post = Post::find(1);
$post->delete();
```

---

## Bonus: Eloquent Relationship Methods Recap

| Relationship | Model Method |
|--------------|---------------|
| One to One   | `hasOne`, `belongsTo` |
| One to Many  | `hasMany`, `belongsTo` |
| Many to One  | `belongsTo` (reverse of hasMany) |

---
