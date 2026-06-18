###### [Webhook](README.md) > Verifying webhook signatures

# Verifying webhook signatures

FarPay signs outgoing webhooks so you can confirm a delivery genuinely originated from FarPay and was not altered in transit. Signing follows the [Standard Webhooks](https://www.standardwebhooks.com) specification.

> **Signatures are only attached when a secret is configured on the webhook** (Settings → Webhooks). Webhook without a secret are sent unsigned. Set a secret to enable verification.
>
> Only JSON and XML webhooks are signed.

# Headers

Every signed delivery carries three headers:

| Header | Example | Description |
|---|---|---|
| `webhook-id` | `whmsg_84213` | Unique id for this webhook. **Stable across retries** — use it as an idempotency key. |
| `webhook-timestamp` | `1718000000` | Unix timestamp (seconds) of the send attempt. |
| `webhook-signature` | `v1,3Q9k8s0Q...` | Space-separated list of `version,signature` pairs. Each signature is a base64-encoded HMAC-SHA256. |

# How verification works

The signature is an HMAC-SHA256 computed over this exact string:

```
{webhook-id}.{webhook-timestamp}.{raw-body}
```

base64-encoded, and each entry in the header is prefixed with its scheme version (`v1`). To verify a webhook:

1. Read `webhook-id`, `webhook-timestamp`, and the **raw request body** — the exact bytes you received.
2. Build the signed string `id.timestamp.body`.
3. Compute `base64(HMAC_SHA256(key, signedString))`, using your webhook secret as the key (see [The secret key](#the-secret-key)).
4. Compare your value against **each** `v1,...` entry in `webhook-signature`, using a constant-time comparison. Accept the request if any entry matches.
5. Reject the webhook if `webhook-timestamp` is too far from the current time (see [Replay protection](#replay-protection)).

> The header can contain more than one signature (e.g. during a secret rotation). Always check against all of them and accept if any matches.

# The secret key

FarPay derives the HMAC key from your configured secret exactly the way the Standard Webhooks reference libraries do:

* If the secret starts with `whsec_`, that prefix is stripped.
* The remainder is **base64-decoded** to obtain the key bytes.
* If the remainder is **not** valid base64, FarPay falls back to using its **raw UTF-8 bytes** as the key.

**Recommendation:** use a `whsec_`-prefixed, base64-encoded secret of at least 24 random bytes. Such a secret works directly with any off-the-shelf Standard Webhooks library. An arbitrary free-text secret still works, but you must verify it manually.

# Replay protection

The `webhook-timestamp` is part of the signed content. You may set your own tollerance for when a webhook shall be invalidated due to age.

# Idempotency

The `webhook-id` is unique per webhook and stays the same across retries.

# Retries

A failed delivery is retried with the **same `webhook-id`** but a **fresh `webhook-timestamp` and signature** for each attempt.

# Testing

Use this published Standard Webhooks vector to confirm your verifier is correct. With the secret `whsec_MfKQ9r8GKYqrTwjUPD8ILPZIo2LaLaSw`, id `msg_p5jXN8AQM9LWM0D4loKWxJek`, timestamp `1614265330`, and body `{"test": 2432232314}`, the signed string is:

```
msg_p5jXN8AQM9LWM0D4loKWxJek.1614265330.{"test": 2432232314}
```

and the expected signature is:

```
v1,g0hM9SsE+OTPJTGt/tmIKtSyZlE3uFJELVlNIOLJ1OE=
```

###### [Webhook](README.md) > Verifying webhook signatures
