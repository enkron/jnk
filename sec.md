# sec
```bash
# PGP - Pretty Good Privacy (Standart)
gpg --decrypt --pinentry-mode=loopback
# return PIN entry to the caller
# (makes possible to entry a PIN inside a shell instead of call annoying window)

gpg --full-generate-key
gpg --list-secret-keys --keyid-format LONG
gpg --armor --export <key_id> # export public part of gpg key in string format
```
```
