# 🔑 Engineering: Domain-Restricted Auth & Asynchronous OTP Pipeline

## 1. Overview

The YSP University platform features a specialized two-tier authentication architecture:
1. **Central Super-Admin Authentication:** Guarded by session-based `AdminAuth` middleware.
2. **Faculty Self-Service Authentication:** Guarded by `EmpAuth` middleware, paired with institutional domain email validation and an asynchronous email OTP verification handshake.

---

## 2. Institutional Domain Validation

To prevent unauthorized public users from creating faculty records, the registration controller enforces domain filtering:

```php
public function checkMail($email)
{
    $exp = explode('@', $email);
    if (isset($exp[1]) && $exp[1] == 'tingebharat.com') {
        return true;
    } else {
        return false;
    }
}
```

---

## 3. Asynchronous OTP Dispatch & Verification Flow

### 3.1 Step 1: Pre-Flight Check & OTP Transmission
When the faculty applicant inputs their email and clicks "Send OTP", client-side jQuery fires an AJAX request to `/sendMailpost`:

```javascript
$.post("/sendMailpost", { email: email }, function (result) {
    if (result == "done") {
        document.getElementById("send-otp-btn").style.display = "none";
        document.getElementById("reg-btn").style.display = "block";
        document.getElementsByClassName("otp-box")[0].style.display = "block";
        toastr.success("OTP has been sent to your email. Please check your email.");
    } else if (result == "err") {
        toastr.error("Only Professional Emails are allowed.");
    } else if (result == "already") {
        toastr.error("You have already registered from this email.");
    }
});
```

On the backend:
```php
$random = rand(10000, 100000);
$req->session()->put('emp_otp', $random);
$req->session()->put('emp_email', $to);

$subject = "Email Verification";
$message = "<html><body><p>Your Email verification OTP is $random</p></body></html>";
$headers = "MIME-Version: 1.0\r\nContent-type:text/html;charset=UTF-8\r\nFrom: <yashin123786@gmail.com>\r\n";
mail($to, $subject, $message, $headers);
```

### 3.2 Step 2: OTP Verification
When the applicant enters the OTP, an AJAX post to `/otpVerify` verifies the payload against the active session:

```php
public function otpVerify(Request $req)
{
    $otp = $req->post('otp');
    $sessionOTP = $req->session()->get('emp_otp');
    if ($otp == $sessionOTP) {
        $req->session()->put('emp_otp_status', "verified");
        echo "match";
    } else {
        echo "error";
    }
}
```

### 3.3 Step 3: Registration Execution
Upon receiving `"match"`, JavaScript submits the parent form. The controller verifies that the email matches `$sessionEmail` and that `$emp_otp_status === "verified"` before hashing the password and saving the employee entity:

```php
$model->password = Hash::make($req->post('password'));
$model->save();
```

---

## 4. Middleware Guards

- **`AdminAuth` Middleware:** Inspects `$request->session()->has('ADMIN_LOGIN')`. Redirects unauthenticated requests to `/admin`.
- **`EmpAuth` Middleware:** Inspects `$request->session()->has('EMP_LOGIN')`. Redirects unauthenticated requests to root `/`.
