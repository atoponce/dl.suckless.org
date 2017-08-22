# Suckless Downloads File Integrity

Every file that is not a website (`htmlout` and `stali/clt2010`) is hashed with
MD5, SHA-1, SHA-256, and SHA-512. Each checksum file is then cryptographically
signed with [Aaron Toponce's public OpenPGP
key](https://keybase.io/atoponce/pgp_keys.asc).

After verifying the checksum, you are encouraged to verify the cryptographic
signature provided with each checksum file.

This is to help ensure file integrity that you have downloaded all the bits
from dl.suckless.org while it is currently served under HTTP, and is still of
value for HTTPS, if deployed.

I am not distributing the software, so you will not get any file downloads from
this Github repository. This repository only serves to provide file integrity
by the software provided at dl.suckless.org.

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
