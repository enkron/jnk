# sec
## Generate new keys

```bash
gpg --full-generate-key
```

## List secret keys
We can use `--list-secret-keys` or its short form `-K` flag to check
imported keys. In order to check key id info as well we'd add
`--keyid-format=long` flag:

```bash
gpg -K --keyid-format=long
```

Alternatively, we can identify a particular private key by its email address:

```bash
gpg -K --keyid-format short user@example.com
```

## Export a secret key
In order to have a file with a secret key for its future transition to
another machine for example - we'd export it to a file:

```bash
gpg --export-secret-keys <GPG_KEY_ID> > private.key
```
### Export public part of gpg key in string format

```bash
gpg --armor --export <GPG_KEY_ID>
```

## Import a secret key
When we have a file with a secret key in the new environment - we can
easily add the key to a keyring:

```bash
gpg --import private.key
```

## File encryption
In order to encrypt a file with a specific key id, we need to provide a
recipient with a `-r/--recipient` flag:

```bash
gpg -r <GPG_KEY_ID> -e <some_file_to_encrypt>
```

## Notes
PGP - Pretty Good Privacy (Standart)
