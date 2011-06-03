Overview
--------

It's dead simple.  Run `pdub`, and you get a blank buffer in vim.  Enter your
passwords and personal info.  Type ":wq", and `pdub` encrypts the buffer and
stores it in your home directory where only you can get to it.  Next time you
run it, `pdub` will decrypt the file, throw that into a buffer for your, and
you're back in business.

`pdub` is a small Python script.  That's good because it keeps things simple,
and no one wants complications when it comes to personal data.

`pdub` doesn't save your decryption passphrase or plain text passwords to any
temporary files.  It doesn't use `gpg`'s "--passphrase" option.  It uses pipes
like a good plumber so your passwords don't get spilled all over the place.

Need to recover your passwords without `pdub`?  Just run the following:

	$ gpg -d ~/.pdub/pdubs.json.gpg


Requirements
------------

 - a POSIX system
 - Python >= 2.6 (RHEL5 be dammned)
 - vim compiled with Pyton support
 - [GnuPG](http://www.gnupg.org/)


Details
-------

`pdub` uses `gpg` with the --symmetric flag for encryption.  The file is stored
in the `~/.pdub` directory.  If this isn't there it creates it for you.  The
directory must have 700 permissions and the actual file is stored with 600
permissions.


Things That Still Need Work
---------------------------

`pdub` assumes that you're storing your passwords in JSON.  Most people
probably don't want that.  There should be some configuration file where users
can specify file types and other preferences (like a .pdubrc).

It would also be cool if `pdub` integrated with Dropbox.  Don't get me wrong,
I'd never put my passwords out there like that, but since it's an encrypted
file there's probably people who would feel safe doing so.
