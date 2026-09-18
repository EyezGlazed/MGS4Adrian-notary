# MGS4 A.D.R.I.A.N. - milestone commitments

This repository publishes cryptographic commitments to a private source
repository, so that its contents at a given date can be proved later without
publishing the source itself.

Each milestone has:

- `<milestone>.commitment.txt` - the manifest hash, the signature hash, the
  signing key and its fingerprint, and the commit and tag ids in the private
  repositories.
- `<milestone>.manifest.txt.sig` - a detached SSH signature over the manifest,
  made before the timestamp below, so the timestamp attests to both.
- `<milestone>.commitment.txt.ots` - an OpenTimestamps proof that the
  commitment file existed by a given date, anchored in a Bitcoin block.
- `allowed_signers` - the public key, for verification.

The manifest itself is **not** published. It lists every filename in the
project. It is disclosed only if and when the source is.

## Verifying

The timestamp needs nothing but the `.ots` file, at
<https://opentimestamps.org>, which reports the Bitcoin block and its time.

The signature needs the manifest, which comes with disclosure:

```
ssh-keygen -Y verify -f allowed_signers -I luggruff@gmail.com -n file \
    -s <milestone>.manifest.txt.sig < <milestone>.manifest.txt
```

The contents need the repositories themselves, also at disclosure. Each
commitment file names the commits to check against.

Signing key fingerprint, also published on the Nexus Mods page:

```
SHA256:pk5S5cpmAd4GmpsqadWx6dr+M8v20QpOG2ZD+T+78Wo
```