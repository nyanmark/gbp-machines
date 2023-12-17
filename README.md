<div align="center">

# Gentoo Build Publisher Machines

</div>

This is a collection of machine definitions and build instructions for [Gentoo
Build Publisher](https://github.com/enku/gentoo-build-publisher), as described
in the [Install
Guide](https://github.com/enku/gentoo-build-publisher/wiki/Install-Guide).
These can be used as a basis for creating your own personal machine
definitions.  The expectation is that you'd fork this repo and just go with
it.

To create a new machine definition simply:

[Fork me on GitHub.](https://github.com/enku/gbp-machines/fork)

```
make mylaptop.machine
```

This will create a new directory, `mylaptop` with a configuration copied from
the `base` machine.  To instead base it off of another previous definition,
say `testing`:

```
make mylaptop.machine base=testing
```

Then make your desired changes to the machine definition.

```
git add mylaptop
git commit -m 'New machine: mylaptop'
git push
```

Then from your GBP instance, create a new job called `mylaptop`.

```
gbp addmachine mylaptop https://github.com/<mygithubuser>/gbp-machines.git
```
Then start building!

```
gbp build mylaptop
```

The following starter machines are included:

- `base` is a from-the-handbook base (systemd) Gentoo install with an empty
  world file.
- `arm64-base` is like base but with an ARM64 target. This is meant to be
   build on an AMD64 machine using [QEMU](https://www.qemu.org/) as the
   [binary format helper](https://en.wikipedia.org/wiki/Binfmt_misc). Because
   of the underlying emulation this machine build runs slower than the other
   builds.
- `testing` is the same as `base` but with `ACCEPT_KEYWORDS=~amd64`
- `gbpbox` is a machine definition per the GBP Install Guide. You can use it
  to have your GBP instance build itself.

Feel free to create and share your own machine definitions.

The `Makefile` does a `gbp pull` instead of `gbp publish`. That's because I
prefer to publish my builds manually. If your preference is to have new builds
publish automatically, simply replace `pull` with `publish`.

By the way, there's nothing dictating that machines in GBP be built a specific
way.  You can build machine artifacts in any manner you want.  As long as the
artifacts have all the
[contents](https://github.com/enku/gentoo-build-publisher/blob/master/docs/artifact-spec.md#gentoo-build-publisher-artifact-specification)
that GBP expects.  This is merely how **I** build my machines but I think it's
a good guide and starting point. Again you are free to go with where ever your
imagination takes you!
