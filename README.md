6th# SecureDroid

A privacy-first Android security toolkit for encrypted files and messages,
safer Wi-Fi usage, and private DNS configuration.

## Goals

- Encrypt and decrypt files using Android’s modern cryptography APIs
- Provide a secure, end-to-end-encrypted message format
- Audit Wi-Fi and network security settings
- Configure Android Private DNS
- Avoid proprietary, closed-source, or custom cryptography
- Keep all private data on-device whenever possible

## Target Platform

- Android 17
- Samsung Galaxy A17 5G
- Kotlin
- Minimum Android SDK: use a conservative supported API level
- Target Android SDK: 37 or the latest official Android 17 SDK

## Scope

### Initial version

- Secure file selection
- Local file encryption
- Password-based key derivation
- Private DNS setup guidance
- Wi-Fi security checklist
- Permission and network-state auditing
- Plain-language security findings

### Future version

- Android-native share-sheet integration
- Encrypted text/clipboard messages
- Optional password-protected exports
- QR-based key exchange
- Certificate and network connection auditing
- Android Keystore-backed key management
- App shortcuts for security profiles
- Wear OS companion, only if useful

## Security Model

The application does not implement custom cryptographic algorithms.

- Use Android Keystore for key generation and storage
- Use AES-GCM for authenticated encryption
- Derive passwords with PBKDF2 or Argon2id
- Generate random values using `SecureRandom`
- Keep plaintext out of logs, backups, notifications, and clipboard
- Authenticate before decrypting private data
- Store only encrypted data and required, non-secret metadata
- Make cryptographic key deletion and app reset explicit
- Test all encrypted-file operations against corruption, truncation, and wrong passwords
- Use OS-level secure storage and Android backup exclusions

> This project is for defensive security. It should not collect data, expose
> keys, bypass device policies, intercept encrypted traffic, or weaken Android
> security controls.

## Recommended Architecture

```text
app/
  ui/
  security/
    keystore/
    encryption/
    password/
  network/
    dns/
    wifi/
  audit/
  data/
  presentation/
magic
format version
algorithm ID
KDF ID
salt
IV
ciphertext
GCM authentication tag