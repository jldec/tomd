# tomd

### Automated conversion from .textile to .md with pandoc

Users with many textile files in their Jekyll Pages site should consider using [pandoc](http://pandoc.org), a utility for converting between different markup formats. E.g. for converting from textile to markdown:

```sh
pandoc --wrap=preserve -f textile -t markdown_github <foo.textile >foo.md
```

##### limitations
Unfortunately pandoc may change content in unwanted ways when it encounters:

- YAML frontmatter at the top of .textile files
- `{% highlight %}` blocks
- `<notextile>` blocks

To get around these limitations, this `tomd` shell script calls [awk](http://www.grymoire.com/Unix/Awk.html) and [sed](http://www.grymoire.com/Unix/Sed.html) to filter out those sections and then re-insert them after pandoc has converted the rest the file.

##### to run `tomd`
Copy `tomd` and the 2 awk scripts from this repo into your jekyll project folder (or a subdirectory if you prefer)

Then invoke with `./tomd`.

```
$ ./tomd
checking for sed, awk, and pandoc
/usr/bin/sed
awk version 20070501
pandoc 1.16.0.2
looking for .textile files in _posts moving them to _old_posts
226 textile files converted
```

#### running under Windows

The latest Pandoc for Windows can be downloaded from https://github.com/jgm/pandoc/releases/.

In addition to pandoc, the `tomd` script requires a unix-y shell and utilities - the easiest way to get those for Windows is by installing the default set of [cygwin](https://cygwin.com/install.html) utilities.

Finally, before running tomd, i had to install `dos2unix` and run it against the `tomd` file to remove extra linefeeds.

Here is the output of running `tomd` against the same repo in the cygwin shell.
```
$ script/tomd
checking for sed, awk, and pandoc
/usr/bin/sed
GNU Awk 4.1.3, API: 1.1 (GNU MPFR 3.1.3, GNU MP 6.1.0)
pandoc.exe 1.16.0.2
looking for .textile files in _posts moving them to _old_posts
226 textile files converted
```
