Mixmaster has long used 1024-bit RSA with a packet format that allows
a maximum of 20 hops; each encrypted with a different RSA key.  The
data for each hop occupies 512 bytes.

Given the declining protection offered by a key size from the 1990s I
decided to investigate adapting mixmaster to use 2048-bit keys (each
in a larger header block) at a cost of reducing the longest chain to
10 hops.

It turned out possible to exceed this goal.  By using a header of
1024 bytes (max 10 hops) new code can use key sizes of 2048, 3072
and 4096 for RSA.  E.g. 10 hops of 4096; or 2 of 1024 and 9 of 4096.
(Key generation might be "mixmaster -G --size=4096 --lifetime=90".)
The default size in the new code is 4096 bits.

The RSA encryption transferred a 3DES key of 24 bytes and otherwise
contained a lot of free space.  Taking advantage of this space to
transfer extra data without growing the packets enabled further progress.

When using the larger RSA keys (2048 and up) the symmetric crypto of
3DES CBC is augmented by adding AES-256 CFB on top of it.  And three
parts of the data are covered by HMAC-SHA256 (in the order encrypt then MAC).
- the body which previously had no protection
- the current header block which had only MD5
- the next header block to prevent a tagging attack (see footnotes)
When using 1024-bit RSA these new features are not used so as to keep
compatibility with older software.

Stats are kept of the RSA key sizes used to help operators monitor uptake of
larger keys and assess when 1024-bit keys can be discontinued.

Actions:
1.  To review and discuss the code please use Mixmaster-devel@lists.sourceforge.net
    (still a  useful place to hold discussion although the SF maintainers are inactive ).
2.  To discuss testing and deployment use Remops@lists.mixmin.net (it would be helpful
    to have some short-term test remailers even if they were not to remain long term.)
    Some traffic may be relevant on both those lists and maybe also cryptography@metzdowd.com .
3.  Development of a more advanced remailer needs a lead maintainer:
    mixminion-dev@seul.org
    http://mixminion.net/
    https://github.com/nmathewson/mixminion

Code location:
http://www.zen19351.zen.co.uk/mixmaster303/

Further reading:
http://www.freehaven.net/anonbib/cache/mixmaster-spec.txt
https://crypto.is/blog/packet_formats_1
https://crypto.is/blog/tagging_attack_on_mixmaster
http://www.nsa.gov/business/programs/elliptic_curve.shtml
