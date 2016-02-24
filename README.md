# tomd
## Automated conversion from .textile to .md with pandoc

Users with many Textile files in their Jekyll Pages site can leverage  [pandoc](http://pandoc.org), a utility for converting between different markup formats.

This [`tomd`](https://github.com/jldec/tomd) shell script uses [awk](http://www.grymoire.com/Unix/Awk.html) and [sed](http://www.grymoire.com/Unix/Sed.html) to overcome the biggest limitations of pandoc, filtering out the sections listed below, which pandoc doesn't recognize, and re-inserting them into the converted Markdown.

- YAML frontmatter at the top of .textile files
- `{% highlight %}` blocks
- `<notextile>` blocks

NOTE: This process may still produce some incorrect output. Known issues include:

- Lost CSS references e.g. from Textile `.p(classname)`
- Literal HTML mixed with unconverted Textile formatting

### To run `tomd`

1. Install pandoc from https://github.com/jgm/pandoc/releases or [here](http://pandoc.org/installing.html).
2. [Download](https://github.com/jldec/tomd/archive/v1.0.zip) or clone this repo.
3. Copy the `tomd` script and the 2 awk files into your Jekyll project.
4. Run the script from inside your Jekyll project folder.
5. Validate the results.

The script will look for any `.textile` files in the `_posts` directory, convert them to `.md`, and leave backups of the original `.textile` files in a new directory called `_old_posts`. You can override the names of the directories with arguments to the script.

If everything works, you should see output like:

```
$ ./tomd
checking for sed, awk, and pandoc
/usr/bin/sed
awk version 20070501
pandoc 1.16.0.2
looking for .textile files in _posts moving them to _old_posts
58 textile files converted
```

##### Running under Windows

The latest version of pandoc for Windows can be downloaded from https://github.com/jgm/pandoc/releases/.

In addition to pandoc, `tomd` requires a unix-y shell and utilities. The easiest way to get those for Windows is by installing the default set of [cygwin](https://cygwin.com/install.html) utilities.

Before running tomd, use cygwin `dos2unix` and run it against the `tomd` file to remove extra linefeeds.

The output of running `tomd` in the cygwin shell should look very similar to the OSX output above.

#### NOTE
`tomd` has run successfully under OSX and Windows against a couple of repos, but it was not extensively tested, so use at your own risk.
Also, please make backups of your content!
