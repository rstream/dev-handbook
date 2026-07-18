# Password hashes in PHP

[← back](../index.md)

Use `password_hash()` to create password hashes.
Use `password_verify()` to check a password against a saved hash.

Do not save plain text passwords.

## Summary

- [Create password hash](#create-password-hash) - `password_hash()` creates a safe hash for storage
- [Verify password](#verify-password) - `password_verify()` checks a login password
- [Rehash old hash](#rehash-old-hash) - `password_needs_rehash()` checks whether a hash should be updated

## Create password hash

```php
$password = $_POST['password'];

$passwordHash = password_hash($password, PASSWORD_DEFAULT);
```

Save `$passwordHash` in the database, not `$password`.

Example insert:

```php
$sql = '
INSERT INTO users (email, password_hash)
VALUES (:email, :password_hash)
';

$stmt = $pdo->prepare($sql);
$stmt->execute([
    'email' => $_POST['email'],
    'password_hash' => $passwordHash,
]);
```

`PASSWORD_DEFAULT` uses the current recommended PHP password hashing algorithm.
The stored column should be long enough for future algorithms.
Use `VARCHAR(255)` or `TEXT`.

## Verify password

Get the saved hash from the database, then compare it with the password from the login form.

```php
$sql = '
SELECT id, email, password_hash
FROM users
WHERE email = :email
';

$stmt = $pdo->prepare($sql);
$stmt->execute([
    'email' => $_POST['email'],
]);

$user = $stmt->fetch(PDO::FETCH_ASSOC);

if ($user !== false && password_verify($_POST['password'], $user['password_hash'])) {
    echo 'Login successful';
} else {
    echo 'Invalid email or password';
}
```

Use the same error message for a missing user and a wrong password.
This avoids revealing which emails are registered.

## Rehash old hash

When PHP changes the default algorithm or options, old hashes can be updated after a successful login.

```php
if (password_verify($_POST['password'], $user['password_hash'])) {
    if (password_needs_rehash($user['password_hash'], PASSWORD_DEFAULT)) {
        $newHash = password_hash($_POST['password'], PASSWORD_DEFAULT);

        $sql = '
        UPDATE users
        SET password_hash = :password_hash
        WHERE id = :id
        ';

        $stmt = $pdo->prepare($sql);
        $stmt->execute([
            'password_hash' => $newHash,
            'id' => $user['id'],
        ]);
    }
}
```

Only rehash after `password_verify()` returns `true`.
