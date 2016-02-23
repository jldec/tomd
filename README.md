# tomd

### Automated conversion from .textile to .md with pandoc

Users with many textile files in their Jekyll Pages site should consider using [pandoc](http://pandoc.org), a utility for converting between different markup formats. E.g. To convert `foo.textile` to `foo.md`

```sh
pandoc --wrap=preserve -f textile -t markdown_github <foo.textile >foo.md
```

##### Limitations
Unfortunately pandoc may change content in unwanted ways when it encounters:

- YAML frontmatter at the top of .textile files
- `{% highlight %}` blocks
- `<notextile>` blocks

To get around these limitations, this [`tomd`](https://github.com/jldec/tomd) shell script calls [awk](http://www.grymoire.com/Unix/Awk.html) and [sed](http://www.grymoire.com/Unix/Sed.html) to filter out those sections and then re-insert them after pandoc has converted the rest the file.

##### To run `tomd`

1. Install pandoc from https://github.com/jgm/pandoc/releases
2. Copy the tomd script and 2 awk files into your Jekyll project and run the script from there.

```
git clone https://github.com/jldec/tomd.git
cp tomd/tomd tomd/*.awk your-jekyll-project-folder
cd your-jekyll-project-folder
./tomd
```

The script will look for `.textile` files in the `_posts` directory, convert them to `.md`, and leave backups of the original `textile` files in a new directory called `_old_posts`. You can override the names of the 2 directories with 2 arguments to the script.

If everything works, you should see output like:

```
$ ./tomd
checking for sed, awk, and pandoc
/usr/bin/sed
awk version 20070501
pandoc 1.16.0.2
looking for .textile files in _posts moving them to _old_posts
nnn textile files converted
```

#### Running under Windows

The latest version of pandoc for Windows can be downloaded from https://github.com/jgm/pandoc/releases/.

In addition to pandoc, `tomd` requires a unix-y shell and utilities. The easiest way to get those for Windows is by installing the default set of [cygwin](https://cygwin.com/install.html) utilities.

Before running tomd, use cygwin `dos2unix` and run it against the `tomd` file to remove extra linefeeds.

The output of running `tomd` in the cygwin shell should look very similar to the OSX output above.

#### NOTE
`tomd` has run successfully under OSX and Windows against a couple of repos, but it was not extensively tested, so use at your own risk.
Also, please make backups of your content!
