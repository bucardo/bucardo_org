---
title: Bucardo boolean
---

Bucardo requires the use of the Perl module named **boolean**. This should be available in your normal packaging system. Try one of:

-   apt-get install libboolean-perl
-   yum install perl-boolean
-   (BSD systems) cd /usr/port/devel/p5-boolean; make install clean

You can also install it directly from CPAN. If you have the CPAN module installed (may need to do `yum install perl-CPAN`), you can simply run:

    sudo cpan boolean

Or with a plenv-based Perl with cpanm you can run:

    cpanm boolean
