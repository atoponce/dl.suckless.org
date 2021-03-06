# Suckless Downloads File Integrity
## Introduction
Every file that is not a website (`htmlout` and `stali/clt2010`) is hashed with
MD5, SHA-1, SHA-256, and SHA-512. Each checksum file is then cryptographically
signed with [Aaron Toponce's public OpenPGP
key](https://keybase.io/atoponce/pgp_keys.asc) and a
[Minisign](https://github.com/jedisct1/minisign) public key for those that
don't want to use OpenPGP.

After verifying the checksum, you are encouraged to verify the cryptographic
signature provided with each checksum file. This is to help ensure file
integrity that you have downloaded all the bits from
[dl.suckless.org](https://dl.suckless.org), and ensure you recevied all the
bits from a trusted source.

I am not distributing the software, so you will not get any file downloads from
this Github repository. This repository only serves to provide file integrity
by the software provided at [dl.suckless.org](https://dl.suckless.org). I am
also not the developer of any of the software, so you may or may not trust me
as an independent 3rd party providing file integrity proofs.

## How To Get and Verify the Software
There are two primary ways to retrieve the software, only one of which provides
automatic file integrity checking:

1. Git
2. HTTPS

### Using Git
Git provides automatic file integrity checking when working in the respository.
For that reason alone, you should probably prefer this method over using
standard HTTPS to get your software.

You can clone any [suckless Git repository](https://git.suckless.org/) one of
three ways:

    $ git clone https://git.suckless.org/<NAME> # preferred
    $ git clone ssh://<USER>@suckless.org/gitrepos/<NAME>
    $ git clone git://git.suckless.org/<NAME>

Using SSH requires that you have an account with the server, but guarantees
file confidentiality in addition to file integrity.

### Using HTTPS
Because file integrity was initially sparse throughout the project, that is
what this Github repository was built for. The project now distributes SHA-256
signatures throughout the project. You should verify the signatures there, and
if still not sure, you could also verify them here.

First, download the tool you want to install, and then the sha256sums.txt file:

    $ wget https://dl.suckless.org/dwm/dwm-6.1.tar.gz
    $ wget https://dl.suckless.org/dwm/sha256sums.txt

Alternatively, using this repository:

    $ wget https://dl.suckless.org/dwm/dwm-6.1.tar.gz
    $ wget https://raw.githubusercontent.com/atoponce/dl.suckless.org/master/dwm/sha256sums.txt

#### Verifying with OpenPGP
The Suckless project does not provide cryptographic authentication with their
sha256sums.txt files, but I do. As such, you can verify my sha256sums.txt.asc
signature with my OpenPGP key:

    $ wget https://raw.githubusercontent.com/atoponce/dl.suckless.org/master/dwm/sha256sums.txt.asc
    $ sha256sum -c --ignore-missing sha256sums.txt
    $ gpg --keyserver hkps://hkps.pool.sks-keyservers.net --recv-keys 0x22EEE0488086060F
    $ gpg --verify sha256sums.txt.asc

#### Verifying with Minisign
Or alternatively, you can verify my sha256sums.txt.minisig signature using
[Minisign](https://github.com/jedisct1/minisign) from Frank Denis for those who
don't want to rely on OpenPGP:

Save the Minisign public key for this project as `minisign.pub` somewhere on
your filesystem:

    RWTjsJ6XZCpZ93yok2PRq2j1pDJj+bzse657NJlN1pywF4Qf6o1cV4Dy

Then verifying the signatures can be done in the following manner:

    $ wget https://raw.githubusercontent.com/atoponce/dl.suckless.org/master/dwm/sha256sums.txt.minisig
    $ sha256sum -c --ignore-missing sha256sums.txt
    $ minisign -Vm sha256sums.txt -p /path/to/minisign.pub 

Or alternatively:

    $ minisign -Vm sha256sums.txt -P RWTjsJ6XZCpZ93yok2PRq2j1pDJj+bzse657NJlN1pywF4Qf6o1cV4Dy

This is the best you can do, until cryptographic digital signatures exist on
the [dl.suckless.org](https://dl.suckless.org) site.
