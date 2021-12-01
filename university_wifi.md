https://www.reddit.com/r/Fedora/comments/jd92gb/wpa2_enterprise_network_no_longer_works_after/

WPA2 enterprise networks largely stopped working after Fedora 33 due to security updates. Replicating the text from this (very helpful!) reddit post):

<blockquote>
Update: So looks like u/GolbatsEverywhere hit the nail on the head. Looks like after setting the phase 2 crypto settings with:

```
update-crypto-policies --set LEGACY 
```

as indicated here: I was able to connect with no issues. Now comes the question of seeing if my work can update their radius server, but that's not for here. Thank you everyone for helping me and being patient!

Thanks to u/GolbatsEverywhere u/vetinari u/anonim_root for sharing some cool information!

</blockquote>

downstream comments
<blockquote>
  Guess: https://fedoraproject.org/wiki/Changes/StrongCryptoSettings2. Your TLS certificate probably uses either SHA-1 (most likely) or RSA-1028 (less likely). Both are rejected now.

Test by downgrading your system policy to allow all crypto that was permitted in Fedora 32:
```
$ sudo dnf install crypto-policies-scripts
$ sudo update-crypto-policies --set DEFAULT:FEDORA32
```
If my guess is wrong, you'll want to revert to secure Fedora 33 default settings:
```
$ sudo update-crypto-policies --set DEFAULT
```
P.S. This might be a pretty lousy guess, because it looks like you are using only password authentication? Eh, worth a try regardless.

P.S.S. Use journalctl -f to check for anything interesting at the time you connect.
 </blockquote>
