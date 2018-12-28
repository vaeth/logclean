# logclean

(C) Martin Väth (mvath at google.com).

This project is under the BSD license 2.0 (“3-clause BSD license”).

With Gentoo, it is a good idea to keep the install logs
of all installed packages.
In case something goes wrong, a `grep` in these logs is sometimes very handy.

However, if you set `PORTAGE_LOGDIR` in your `make.conf`, you soon have also
thousands of logs of obsolete packages, because each `emerge`
(successful or not) and also each `unmerge` (even fast `unmerge`)
produces a logfile.

The purpose of this project is to eliminate all logs except for the
newest installation logs for the actually installed packages;
the used ones are compressed using brotli, zstd, xz, lzma, bzip2, or gzip,
and selected ones (determined by `/etc/logclean.conf`) are even shortened.
Moreover, by default all color sequences are removed.

This script takes care in a similar way about your files in
- `/var/log/elogs` (cf. the `ELOG` feature of __portage__)
- `/var/log/notices` (cf. the unofficial __enotice__ script)

This script can also cleanup your temporary installation directories in
- `/var/tmp/portage` (do not use this in a cron job if __portage__
  might be running).

Finally, this script can also shorten the main portage logfile
- `/var/log/emerge.log`

so that only the actually installed packages are logged.
(You might want to keep these for usage with `qlop` or `genlop`).

This script is also offers option for a convenient usage from a cron job.

If you have installed `app-portage/eix`, this script will run slightly faster.

### Installation

For installation, copy the content of `bin/` with executable permission in your
`$PATH` (perhaps `/usr/bin/`) and the (possible edited) content of `etc/`
to `/etc/`.

To obtain support for __zsh completion__, you can copy the content of `zsh/`
to a directory of your zsh's `$fpath`
(perhaps `/usr/share/zsh/site-functions/`).

For installation under Gentoo, there is an ebuild in the `mv` repository
(available by `app-select/eselect-repository` or `app-portage/layman`).
