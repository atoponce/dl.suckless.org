# Suckless Downloads File Integrity

Every file that is not a website (`htmlout` and `stali/clt2010`) is hashed with
MD5, SHA-1, SHA-256, and SHA-512. Each checksum file is then cryptographically
signed with [Aaron Toponce's public OpenPGP
key](https://keybase.io/atoponce/pgp_keys.asc) and a
[Minisign](https://github.com/jedisct1/minisign) public key for those that
don't want to use OpenPGP.

After verifying the checksum, you are encouraged to verify the cryptographic
signature provided with each checksum file.

This is to help ensure file integrity that you have downloaded all the bits
from [dl.suckless.org](http://dl.suckless.org) while it is currently served
under HTTP, and is still of value for HTTPS, if deployed.

I am not distributing the software, so you will not get any file downloads from
this Github repository. This repository only serves to provide file integrity
by the software provided at [dl.suckless.org](http://dl.suckless.org).

## How To Get and Verify the Software

There are two primary ways to retrieve the software, one of which provides
automatic file integrity checking:

1. Git
2. HTTP

### Using Git

Git provides automatic file integrity checking when working in the respository.
For that reason alone, you should probably prefer this method over using
standard HTTP to get your software.

You can clone any [suckless Git repository](http://git.suckless.org/) one of
three ways:

    $ git clone ssh://<USER>@suckless.org/gitrepos/<NAME> # preferred
    $ git clone git://git.suckless.org/<NAME>
    $ git clone http://git.suckless.org/<NAME>

Using SSH requires that you have an account with the server, but guarantees
file confidentiality in addition to file integrity.

### Using HTTP

Because file integrity is sparse throughout the project, that is what this
Github repository is for. HTTP does not provide file integrity, so you will
need to verify the software manually.

First, download the tool you want to install, and a checksum file, such as the
sha256sums.txt:

    $ wget http://dl.suckless.org/dwm/dwm-6.1.tar.gz
    $ wget https://raw.githubusercontent.com/atoponce/dl.suckless.org/master/dwm/sha256sums.txt

#### Verifying with OpenPGP
You can verify the sha256sums.txt.asc signature with OpenPGP:

    $ wget https://raw.githubusercontent.com/atoponce/dl.suckless.org/master/dwm/sha256sums.txt.asc
    $ sha256sum -c --ignore-missing sha256sums.txt
    $ gpg --keyserver hkps://hkps.pool.sks-keyservers.net --recv-keys 0x22EEE0488086060F
    $ gpg --verify sha256sums.txt.asc

#### Verifying with Minisign
Or alternatively, you can verify the sha256sums.txt.minisig signature using
[Minisign](https://github.com/jedisct1/minisign) from Frank Denis for those who
don't want to rely on OpenPGP:

Save the Minisign public key for this project as `minisign.pub` somewhere on
your filesystem:

    RWTjsJ6XZCpZ93yok2PRq2j1pDJj+bzse657NJlN1pywF4Qf6o1cV4Dy

Then verifying the signatures can be done in the following manner:

    $ wget https://raw.githubusercontent.com/atoponce/dl.suckless.org/master/dwm/sha256sums.txt.minisig
    $ sha256sum -c --ignore-missing sha256sums.txt
    $ minisign -Vm sha256sums.txt -p /path/to/minisign.pub 
    Signature and comment signature verified
    Trusted comment: timestamp:1503680772	file:sha256sums.txt

This is the best you can do, until the checksums and digital signatures exist
on the [dl.suckless.org](http://dl.suckless.org) site.

## WARNING

Because the files were downloaded over HTTP, there is no guarantee that the
files I downloaded were not changed as part of a man-in-the-middle attack. As
such, the checksums provided may not match what you receive. I have not
compiled and executed any of software I downloded, so I cannot provide any
guarantees about their accuracy.

So, if your checksum disagrees with what I have provided, either:

1. I did not download all the correct bits, and have a partial download.
2. You did not download all the correct bits.
3. I was the victim of a MITM attack.
4. You were the victim of a MITM attack.

As such, please get in contact with me, and I'll help investigate why there is
a disagreement in our checksums.
