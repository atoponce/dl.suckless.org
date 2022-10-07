# Suckless Downloads File Integrity
## Introduction
Every file that is not a website (`htmlout` and `stali/clt2010`) is hashed with
MD5, SHA-1, SHA-256, and SHA-512. Each checksum file is then cryptographically
signed with Aaron Toponce's public [OpenPGP](https://openpgp.org) key and a public
[Minisign](https://github.com/jedisct1/minisign) key for those that don't want to use
OpenPGP.

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

#### Verifying with OpenPGP
The Suckless project does not provide cryptographic authentication with their
sha256sums.txt files, but I do. As such, you can verify my sha256sums.txt.asc
signature with my [OpenPGP](https://openpgp.org) key. Import my PGP key below, then execute:

    $ wget https://raw.githubusercontent.com/atoponce/dl.suckless.org/master/dwm/sha256sums.txt.asc
    $ sha256sum -c --ignore-missing sha256sums.txt
    $ gpg --verify sha256sums.txt.asc

#### PGP key
    -----BEGIN PGP PUBLIC KEY BLOCK-----

    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
    nVdjAJ48q4lmYqCcTzos+N/wm+M818IcbA==
    =yj1I
    -----END PGP PUBLIC KEY BLOCK-----
