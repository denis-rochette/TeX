# A macOS (10.12) minimal plain TeX using TeX Live and luatex

_This is a personal project, it may not work on another mac. But you can try, nothing is installed anywhere else._


## Installation

Go to the dowloaded directory

```bash
$ echo 'PATH=$PATH:'"$(pwd)/bin/" >> ~/.bashrc
$ source ~/.bashrc
```

### Metafont memory dump files

```bash
$ mf -ini '\input plain; input modes; dump'
$ mv plain.base ./mf/base/
$ echo 'alias mf="mf -base=plain"' >> ~/.bashrc
$ source ~/.bashrc
```

### Fonts

This must be repeated for every font.

```bash
$ mf "\mode:=localfont; input cmr10"
$ gftopk cmr10.600gf
$ mv cmr10.600gf ./font/gf/
$ mv cmr10.600tfm ./font/tfm/
$ mv cmr10.600pk ./font/pk/
```

The following should works

```bash
$ for i in $(ls ./mf/input/cm*[0-9].mf); do mf "\mode:=localfont; input $(basename $i)"; done
$ mf "\mode:=localfont; input manfnt"
$ for i in $(ls ./*gf); do gftopk "./$(basename $i)"; done
$ mv *gf ./font/gf/
$ mv *tfm ./font/tfm/
$ mv *pk ./font/pk/
```

### TeX memory dump files

```bash
$ luatex -ini '\input plain \input luatex \dump'
$ mv plain.fmt ./tex/fmt/
$ echo 'alias tex="luatex --output-format=pdf -fmt=plain"' >> ~/.bashrc
$ source ~/.bashrc
```

### ls-R

Every `.log` files (and other temporary files) must be deleted.

```bash
$ ls -ALR > ls-R
```

### Minimal test

Create a hello.tex file with

```
Hello world
$$
Y = \lambda f.(\lambda x.f\,(x\,x))\,(\lambda x.f\,(x\,x))
$$
\bye
```

then

```bash
tex hello.tex
```


## ls-R

*ls-R* database files need to be updated when the texmf tree change.


## TODO

Compile TeX Live from the source files, notably to change the banner, and disable every mktex scripts.
