# putty-cng

You like putty-cng and you use it on a daily basis? Consider to donate a small amount for the open soure work...

Putty with CryptoAPI (CAPI/CNG) based smartcard implementation.

It's based on PuTTYwincrypt by Ulf Risk (https://github.com/ufrisk/puttywincrypt)
The original PuTTY is found at: http://www.chiark.greenend.org.uk/~sgtatham/putty/

Except for Windows certificate store integration pageant-cng is identical to PuTTY.

<img src="https://gist.githubusercontent.com/ufrisk/8dec5a98bcf875a6254f9e3aa35d12a0/raw/edad0efadd158d1226ebbf4d5587ed4b69f68242/putty_auth.png" height="250"/><img src="https://gist.githubusercontent.com/ufrisk/8dec5a98bcf875a6254f9e3aa35d12a0/raw/edad0efadd158d1226ebbf4d5587ed4b69f68242/putty_pageant_addcert.png" height="250"/>

Download
========
Download the binaries and the patch file stored in the root folder of this repository.

Pageant-cng Usage
==================
Start Pageant by clicking on it. To add a key stored in Windows crypto API right click on Pageant in the systray and select "Add Certificate" in the menu. Whenever the private key is accessed the user may or may not be prompted by Windows to enter a passphrase/PIN depending on whether the key is protected or not.

Please note that it is not possible to add keys backed by Windows from the Pageant main GUI at the moment, only from the systray menu.

To export the public key in the ssh authorized_keys format load the key into Pageant and double click on it. The public key will be copied into the clipboard in the authorized_keys format.

PuTTY-cng Usage
================
To use a key backed by Windows please specify this key in the "Private key file for authentication:" text box found in PuTTY-cng. This text box is found at Connection > SSH > Auth.

To select ANY key backed by Windows type (in the text box):

`cert://*`

In order to select a specific key by certificate thumbprint type:

`cert://thumbprint=<thumbprint_in_hex>`

In order to select a specific key by part of certificate common name type:

`cert://cn=<part_of_common_name_to_search_for>`

Searching for all certificates may take a long time and "hang" PuTTY-cng if there exist many certificates on slow smart cards in the certificate store.

Background
==========
The PuTTY-cng patch was created in order to ease the use of windows store certificates for SSH authentication (including smartcards). The easiest way to go with this seemed to be using the windows crypto api for this. This enabled PuTTY-cng to function without bothering with any direct card drivers and pkcs#11 implementations. PuTTY-cngs also works for soft certificates and keys as well as with other non-smartcard hardware devices.

Version History
===============

v0.77-pre
  - Update upstream PuTTY (version 0.77-pre)
 