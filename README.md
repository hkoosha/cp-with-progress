# cp-with-progress
Gool ol' cp with progress in percent for each file (not total).

## Please note

I don't have time to create patch right now. The added functionallity is not even fully tested, 
I was playing around with coreutils in fedora 22 (the source RPM). But hey! it was fun and kind-of
works.
The total progress is not calculated, just for each file.

I used coreutils version 8.23.

# What about existing tools?

- Are you aware of `rsync`?
-> I most certainly am.

## How to

I'll describe it for fedora 22, but if you got your hands on on coreutils source and found the 
file `copy.c` then it's very likely you'll be able to do it youself. just find the function 
`sparse_copy()` and you are good to go (there is one more for non-sparse I haven't patched).

- downlaod coreutils SRPM from fedora 22.
- exract it, let's assume it'll be extracted to $EXTRACTION_PATH.
- replace the files in $EXTRACTION_PATH/src/ with files in this repo.
- or simply add the necessary code to the file copy.c, comparing with file in this repo.
- run `./configure && make` in $EXTRACTION_PATH
- ~~replace or~~ move the compiled cp command and it's necessary files to ~/.local/bin. **Under NO Circumstance** do replace the system cp with this one.
- make sure ~/.local/bin is looked for executables before /usr/bin.

## Test

create a big file like so: `dd if=/dev/urandom of=random_dummy_data bs=1M count=1000`
with your new cp command, test it like so:

~/.local/bin/cp ~/random_dummy_data ./random_dummy_data_cp

If your drive is too fast (lucky you!) make the file larger so you'll see the result. Or just use an slow medium.
the files random_dummy_data and random_dummy_data_cp will be replaces, I hopy you don't have a file with these names!
instead of ~/.local/bin/cp you can simply run `cp` if `~/.local/bin/` is in your path before `/usr/bin` (or 
wherever your distro/package-manager/yourself) put original `cp`.

good luck.
