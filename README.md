# Password Manager

A local desktop password manager with a Tkinter GUI. Stores encrypted credentials per service, protected behind a master password. All data stays on your machine.

## Features
- Master password authentication with SHA-256 hashing
- Fernet symmetric encryption for all stored passwords
- Add, view, and delete credentials per service
- Built-in password generator with configurable length
- Persistent local storage via JSON

## Requirements
```
cryptography
```
Tkinter is included with standard Python 3 installations.

```
pip install cryptography
```

## Usage
Run the script directly (not as a notebook cell):
```
python password_manager.py
```
On first launch, you'll be prompted to set a master password. On subsequent launches, you must enter the correct master password to unlock the vault.

## How It Works
1. **Master password** is hashed with SHA-256 and stored in `master.hash`
2. A **Fernet key** is generated once and saved to `secret.key` — used to encrypt/decrypt all passwords
3. Credentials are stored encrypted in `passwords.json`

## Local Files Created
| File | Purpose |
|---|---|
| `master.hash` | SHA-256 hash of your master password |
| `secret.key` | Fernet encryption key |
| `passwords.json` | Encrypted credential store |

> ⚠️ **Do not delete `secret.key`** — losing it makes stored passwords unrecoverable.

## Technical Details
- **Encryption:** Fernet (AES-128-CBC + HMAC-SHA256)
- **Master password storage:** SHA-256 hash only — never stored in plaintext
- **Password generation:** Random mix of letters, digits, and punctuation (default 12 chars)
- **GUI:** Tkinter with `ScrolledText` for credential display

## Limitations
- Single-user only — no multi-profile support
- `secret.key` is stored unprotected on disk; anyone with file access can decrypt `passwords.json`
- No clipboard copy button — passwords are displayed in plaintext in the view window
- SHA-256 without salt is used for master password hashing — consider bcrypt/argon2 for production use
- No backup or export functionality

## License
MIT
