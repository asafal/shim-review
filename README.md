This repo is for review of requests for signing shim.  To create a request for review:

- clone this repo
- edit the template below
- add the shim.efi to be signed
- add build logs
- commit all of that
- tag it with a tag of the form "myorg-shim-arch-YYYYMMDD"
- push that to github
- file an issue at https://github.com/rhboot/shim-review/issues with a link to your branch

Note that we really only have experience with using grub2 on Linux, so asking
us to endorse anything else for signing is going to require some convincing on
your part.

Here's the template:

-------------------------------------------------------------------------------
What organization or people are asking to have this signed:
-------------------------------------------------------------------------------
TrulyProtect

-------------------------------------------------------------------------------
What product or service is this for:
-------------------------------------------------------------------------------
The shim will load our secure thin hypervisor which builds a secure execution environment,
used to support our products.
TrulyProtect Execution Protection - Endpoint security product 
TrulyProtect Native Decryption - Software encryption product

-------------------------------------------------------------------------------
What's the justification that this really does need to be signed for the whole world to be able to boot it:
-------------------------------------------------------------------------------
We have clients who wish to install our product on physical machines currently using secure-boot, we do not wish to disable secure boot on these machines in order to get our product running

-------------------------------------------------------------------------------
Who is the primary contact for security updates, etc.
-------------------------------------------------------------------------------
- Name: Asaf Algawi
- Position:
- Email address: asaf@trulyprotect.com
- PGP key, signed by the other security contacts, and preferably also with signatures that are reasonably well known in the linux community:

-------------------------------------------------------------------------------
Who is the secondary contact for security updates, etc.
-------------------------------------------------------------------------------
- Name: Roee Leon
- Position:
- Email address: roee@trulyprotect.com
- PGP key, signed by the other security contacts, and preferably also with signatures that are reasonably well known in the linux community:

-------------------------------------------------------------------------------
What upstream shim tag is this starting from:
-------------------------------------------------------------------------------
15
51413d1deb0df0debdf1d208723131ff0e36d3a3

-------------------------------------------------------------------------------
URL for a repo that contains the exact code which was built to get this binary:
-------------------------------------------------------------------------------
https://github.com/rhboot/shim/tree/51413d1deb0df0debdf1d208723131ff0e36d3a3

-------------------------------------------------------------------------------
What patches are being applied and why:
-------------------------------------------------------------------------------
None.

-------------------------------------------------------------------------------
What OS and toolchain must we use to reproduce this build?  Include where to find it, etc.  We're going to try to reproduce your build as close as possible to verify that it's really a build of the source tree you tell us it is, so these need to be fairly thorough. At the very least include the specific versions of gcc, binutils, and gnu-efi which were used, and where to find those binaries.
-------------------------------------------------------------------------------
Pop OS (Latest version)
GCC-8
built using the following commandline:
make CC=gcc-8 RELEASE=trulyprotect VENDOR_CERT_FILE=../tp.cer DEFAULT_LOADER=tp.efi

-------------------------------------------------------------------------------
Which files in this repo are the logs for your build?   This should include logs for creating the buildroots, applying patches, doing the build, creating the archives, etc.
-------------------------------------------------------------------------------
build.logs

-------------------------------------------------------------------------------
Add any additional information you think we may need to validate this shim
-------------------------------------------------------------------------------
This shim is used to load our thin secure hypervisor, it does not load any unauthenticated application, it will infact load windows boot manager efi, the loading process is done via EFI loadImage and startImage, and therefore does not violate secure boot.
