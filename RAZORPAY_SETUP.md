# Razorpay Setup

AK.Payments integrates with [Razorpay](https://razorpay.com) for payment processing. The API keys are **not** included in this repository — you must supply your own test credentials before running the stack.

---

## 1. Create a Razorpay account and get test keys

1. Sign up (free) at **https://dashboard.razorpay.com/signup**
2. Stay in **Test Mode** (toggle in the top-right of the dashboard)
3. Go to **Settings → API Keys → Generate Test Key**
4. Copy both values:
   - **Key ID** — starts with `rzp_test_`
   - **Key Secret** — shown once at generation time; store it securely

---

## 2. Set the keys — local development

Open `AK.Payments/AK.Payments.API/appsettings.json` and replace the placeholders:

```json
"Razorpay": {
  "KeyId": "rzp_test_YOUR_KEY_ID_HERE",
  "KeySecret": "YOUR_KEY_SECRET_HERE"
}
```

---

## 3. Set the keys — Docker Compose

Open `docker-compose.yml` and replace the placeholders in the `antkart-payments-api` service block:

```yaml
Razorpay__KeyId: "rzp_test_YOUR_KEY_ID_HERE"
Razorpay__KeySecret: "YOUR_KEY_SECRET_HERE"
```

---

## 4. Test cards (Razorpay sandbox)

| Card number | Network | OTP |
|-------------|---------|-----|
| 4111 1111 1111 1111 | Visa | 1234 1234 |
| 5267 3169 4984 2643 | Mastercard | 1234 1234 |

Use any future expiry date and any 3-digit CVV.

---

## 5. Never commit real keys

`appsettings.json` and `docker-compose.yml` are tracked by git. Keep the `YOUR_RAZORPAY_TEST_KEY_*` placeholders in those files and supply real values only via:

- **Local dev:** `dotnet user-secrets set "Razorpay:KeyId" "rzp_test_..."` inside `AK.Payments/AK.Payments.API/`
- **CI / production:** environment variables or a secrets manager
