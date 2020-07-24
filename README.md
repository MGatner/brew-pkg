# brew-pkg

brew-pkg is a Homebrew [external command](https://docs.brew.sh/External-Commands)
that builds a macOS installer package from a [formula](https://formulae.brew.sh).

## Usage

The formula must first already be installed on the system. Using [nginx](https://formulae.brew.sh/formula/nginx) as an example:

`brew pkg nginx`
<code><pre>==> Creating package staging root using Homebrew prefix /usr/local
==> Staging formula nginx
==> Plist found at homebrew.mxcl.nginx, staging for /Library/LaunchDaemons/homebrew.mxcl.nginx.plist
==> Building package nginx-1.2.6.pkg</pre></code>

It can also automatically include the formula's dependencies:

`brew pkg --with-deps --without-kegs ffmpeg`
<code><pre>==> Creating package staging root using Homebrew prefix /usr/local
==> Staging formula ffmpeg
==> Staging formula pkg-config
==> Staging formula texi2html
==> Staging formula yasm
==> Staging formula x264
==> Staging formula faac
==> Staging formula lame
==> Staging formula xvid
==> Building package ffmpeg-3.1.1.pkg</pre></code>

By default behaviour brew pkg include all package kegs located in **/usr/local/Cellar/packagename**.
If you need to exclude it, specify the option `--without-kegs`.

## Installing it

`brew-pkg` is available from this [formulae tap](https://github.com/mgatner/homebrew-pkg). Add the tap:

`brew tap mgatner/pkg`

Then install as any other formula:

`brew install brew-pkg`

## Extras

If a formula has defined a **launchd** plist, brew-pkg will also install this to the package's root in `/Library/LaunchDaemons`.

You can also define a custom identifier prefix in the reverse-domain convention with the `--identifier-prefix` option,
e.g. `brew pkg --identifier-prefix org.nagios nrpe`. If there is a **launchd** plist defined, this same prefix is currently _not_ applied to the plist.

You can set the path to custom **preinstall** and **postinstall** scripts with the `--scripts` option which passed through to the `pkgbuild` command.  
For more information refer to `man pkgbuild` which explains:

> `--scripts scripts_path` archive the entire contents of scripts-path as the package scripts. If this directory contains scripts named preinstall and/or postinstall, these will be run as the top-level scripts of the package [...]

## License

brew-pkg is [MIT-licensed](https://github.com/mgatner/homebrew-pkg/blob/develop/LICENSE.md).

This project began with [Tim Sutton](https://github.com/timsutton/brew-pkg) then was taken over by
[Daniel Bair](https://github.com/danielbair/homebrew-pkg) before landing here. Original repos may
have commits or forks worth reviewing.
