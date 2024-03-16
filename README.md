# dockah : A Fill-in-the-Gaps CLI for `docker`

I have finally cracked the code on asymmetric authentication in
Docker Registries, allowing a public-pull / authenticated-push
architecture so useful to consultancies and open source shops.

However, I found that the standard `docker` CLI was unable to help
me explore the "extra" parts of the [distribution/distribution][1]
API, like `/v2/_catalog` and friends.  So I wrote `dockah`.

[1]: https://github.com/distribution/distribution

## Commands

You can do four things with this CLI tool:

- `dockah catalog` - Shows the catalog endpoint.

  Also known as `dockah cat` for short.

- `dockah tags IMAGE` - Lists all tags for the named image.

- `dockah manifests IMAGE TAG` - Lists all manifests for the given
  image at the specified tag.

  Also known as `dockah show`.

- `dockah remove IMAGE TAG` - Removes an image from the
  repository.  Under the hood this uses an extra API call to
  resolve the tag _name_ into a _digest reference_.

  Also known as `dockah rm`

All four of these interactions with a remote registry will obey
the Www-Authenticate headers sent back by the registry, and will
run credentials through any identified token endpoints.

## Installation

It's straightforward:

```console
$ cp dockah ~/bin/dockash
```

or, if you prefer to inflict this system-wide:

```console
# cp dockah /usr/local/bin
```

The git repo should retain the executable bit on the permissions,
but if it doesn't work out of the box, try that?

## Development

I may not have covered all possible configurations, but it does
work for my small token server implementation, and that's good
enough for now. Feel free to PR changes that make this work in
your setup.

On that note, this is a _side project_ and likely won't merit a
ton of attention unless something breaks that affects me and my
asymmetric setup.  Please don't take it personally if your issues
go untriaged and your PRs go unreviewed.
