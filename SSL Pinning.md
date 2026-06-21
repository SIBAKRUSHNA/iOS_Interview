
# 🔒 SSL Pinning in iOS
<img width="1024" height="1536" alt="ChatGPT Image Jun 21, 2026, 10_34_09 PM" src="https://github.com/user-attachments/assets/966812cf-c229-4382-870d-6d430e9b7a9f" />

## What is SSL Pinning?

SSL Pinning is a security technique used to ensure that an iOS application communicates only with a trusted server.

Instead of trusting any certificate signed by a trusted Certificate Authority (CA), the app validates a specific server certificate or public key embedded within the application.

### Purpose
Protects against **Man-in-the-Middle (MITM)** attacks.

---

# Why SSL Pinning?

Without SSL Pinning:

- App trusts all certificates issued by trusted CAs.
- A compromised CA can issue fraudulent certificates.
- Attackers may intercept network traffic.

With SSL Pinning:

- Only predefined certificates/public keys are trusted.
- Unauthorized certificates are rejected.
- Communication remains secure even if a CA is compromised.

---

# Types of SSL Pinning

## 1. Certificate Pinning

The entire server certificate is stored in the application and compared against the server certificate during the SSL handshake.

### Advantages

✅ Easy to implement

### Disadvantages

❌ App update required whenever certificate changes

---

## 2. Public Key Pinning

Only the server's public key is stored and validated.

### Advantages

✅ More flexible

✅ Certificate can be renewed without updating the app

### Disadvantages

❌ Slightly more complex implementation

---

# Certificate Pinning vs Public Key Pinning

| Feature | Certificate Pinning | Public Key Pinning |
|----------|--------------------|--------------------|
| Pins Entire Certificate | ✅ | ❌ |
| Pins Public Key | ❌ | ✅ |
| Certificate Renewal Impact | High | Low |
| Flexibility | Low | High |
| Recommended Approach | ❌ | ✅ |

---

# SSL Pinning Workflow

```text
App Request
     │
     ▼
Server Sends Certificate
     │
     ▼
URLSession Delegate
     │
     ▼
Extract Certificate/Public Key
     │
     ▼
Compare With Local Pin
     │
 ┌───┴───┐
 │ Match │
 └───┬───┘
     │
     ▼
Allow Connection

No Match
     │
     ▼
Reject Connection
```

---

# Key Classes Used

## URLSessionDelegate

Handles authentication challenges during network requests.

```swift
func urlSession(
    _ session: URLSession,
    didReceive challenge: URLAuthenticationChallenge,
    completionHandler: @escaping (URLSession.AuthChallengeDisposition, URLCredential?) -> Void
)
```

---

## URLAuthenticationChallenge

Represents an authentication challenge received from the server.

Used for:

- SSL Validation
- SSL Pinning
- Certificate Verification

---

## SecTrust

Represents the server trust object.

```swift
let serverTrust = challenge.protectionSpace.serverTrust
```

Used to:

- Evaluate certificate chain
- Verify server trustworthiness

---

## SecCertificate

Represents a certificate in Apple's Security framework.

```swift
let certificate = SecTrustGetCertificateAtIndex(serverTrust, 0)
```

---

# Certificate Pinning Process

### Step 1

Download the server certificate (`.cer`).

### Step 2

Add certificate to the application bundle.

### Step 3

Receive server certificate during SSL handshake.

### Step 4

Compare server certificate with local certificate.

### Step 5

Allow connection only if they match.

---

# Public Key Pinning Process

### Step 1

Extract public key from server certificate.

### Step 2

Store expected public key hash in the app.

### Step 3

Compare server public key with stored hash.

### Step 4

Trust only matching public keys.

---

# Man-in-the-Middle (MITM) Attack

```text
App  <--->  Attacker  <--->  Server
```

An attacker intercepts communication and can:

- Read sensitive data
- Modify requests
- Steal credentials

SSL Pinning helps prevent these attacks.

---

# Certificate Rotation

Certificate rotation is the process of replacing an expired certificate with a new one.

### Best Practices

- Use Public Key Pinning
- Maintain backup pins
- Pin multiple certificates if needed

---

# App Transport Security (ATS)

ATS is an iOS security feature introduced in iOS 9.

It enforces:

- HTTPS connections
- Strong TLS versions
- Secure cipher suites

SSL Pinning provides an additional security layer on top of ATS.

---

# Common SSL Pinning Mistakes

❌ Pinning expired certificates

❌ Ignoring certificate rotation

❌ Comparing certificate names only

❌ Trusting every certificate

Bad Example:

```swift
completionHandler(
    .useCredential,
    URLCredential(trust: serverTrust)
)
```

The above code trusts all certificates without validation.

---

# Testing SSL Pinning

Tools commonly used:

- Charles Proxy
- Burp Suite
- Proxyman
- Fiddler

Expected Result:

```text
Without Pinning:
✅ Connection Succeeds

With Pinning:
❌ Connection Fails
```

---

# Can SSL Pinning Be Bypassed?

Yes, especially on:

- Jailbroken devices
- Frida
- Objection
- Runtime hooking tools

SSL Pinning significantly improves security but is not 100% foolproof.

---

# Frequently Asked Interview Questions

### Beginner

- What is SSL Pinning?
- Why is SSL Pinning used?
- What is a MITM attack?
- What is ATS?
- What is URLSessionDelegate?

### Intermediate

- SSL vs SSL Pinning?
- Certificate Pinning vs Public Key Pinning?
- How is SSL Pinning implemented in iOS?
- What is URLAuthenticationChallenge?
- What is SecTrust?

### Advanced

- How do you handle certificate rotation?
- Why is Public Key Pinning preferred?
- How do you test SSL Pinning?
- Can SSL Pinning be bypassed?
- How would you implement SSL Pinning using URLSession?

---

# One-Line Interview Answer

> SSL Pinning is a security mechanism that validates a server's certificate or public key against a trusted value embedded in the app, protecting against Man-in-the-Middle (MITM) attacks even when a Certificate Authority is compromised.
