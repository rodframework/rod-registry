# rod-registry

The Rod module index (architecture.md Sec 15.2 of the platform
repository): one JSON file per module under `modules/`, contributed by
pull request, no server, no database. A static git repository in the
Homebrew-tap shape -- an optional GitHub Pages mirror may sit beside it,
but the repository is the index.

## Adding or updating a module

From a module checkout:

```
rod mod publish --registry <path-to-this-checkout>
```

Review the entry under `modules/<name>.json`, commit, and open the pull
request. Entries carry the publisher's Ed25519 public key and the
signature over the package's canonical form, plus the package digest;
operators pin the key in their lock file at first install and verify
offline with `rod mod verify`. Publishing the same version with a
different package is refused here and in the tooling -- bump the
version.

## Governance

The canonical rod-registry lives under the
[rodframework](https://github.com/rodframework) organization: entries
land by pull request with review, and merge rights are held by the
organization. Third-party taps are legitimate registries of their own
(`--registry` takes any git URL); this one is the default.
