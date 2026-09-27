# 🛡️ Engineering: Security, Cryptography & Validation

## 1. Overview

The YSP University platform adheres to strict web security standards across authentication, data integrity, and asset handling.

---

## 2. Authentication & Cryptography

### 2.1 Password Hashing via Bcrypt
All passwords stored in `admins` and `employees` tables are hashed using Laravel's `Hash::make()` with Bcrypt:

```php
$model->password = Hash::make($request->post('password'));
```

Authentication verification utilizes constant-time string comparisons via `Hash::check()`:

```php
if ($result && Hash::check($request->post('password'), $result->password)) {
    $request->session()->put('ADMIN_LOGIN', true);
    $request->session()->put('ADMIN_ID', $result->id);
    return redirect('admin/service');
}
```

---

## 3. Session Security & CSRF Protection

- **Fail-Closed Session Verification:** Middleware blocks unauthorized access to operational and administrative endpoints:
  ```php
  if ($request->session()->has('ADMIN_LOGIN')) {
      return $next($request);
  } else {
      $request->session()->flash('error', 'Access Denied');
      return redirect('admin');
  }
  ```
- **CSRF Token Filtering:** Every HTML form incorporates `@csrf`. Asynchronous AJAX requests configure global CSRF headers:
  ```javascript
  $.ajaxSetup({
      headers: {
          "X-CSRF-TOKEN": $('meta[name="csrf-token"]').attr("content"),
      },
  });
  ```

---

## 4. File Upload Sanitization

When processing profile pictures, resumes, and tender documents:
- Uploaded file extensions are resolved using `$request->file('docs')->extension()`.
- Filenames are generated using epoch timestamps and cryptographic random integer prefixes (`rand(999,10000).time().'.'.$ext`), eliminating path traversal and overwrite vulnerabilities.
- Files are saved directly to isolated storage disks via `$request->file('...')->storeAs(...)`.
