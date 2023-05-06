[![Actions Status](https://github.com/skaji/change-shebang/actions/workflows/test.yml/badge.svg)](https://github.com/skaji/change-shebang/actions)

# NAME

App::ChangeShebang - change shebang lines for relocatable perl

# SYNOPSIS

    > change-shebang /path/to/bin/script.pl

    > head -3 /path/to/bin/script.pl
    #!/bin/sh
    exec "$(dirname "$0")"/perl -x "$0" "$@"
    #!perl

# DESCRIPTION

[change-shebang](https://metacpan.org/pod/change-shebang) changes shebang lines from

    #!/path/to/bin/perl

to

    #!/bin/sh
    exec "$(dirname "$0")"/perl -x "$0" "$@"
    #!perl

Why do we need this?

Let's say you build perl with relocatable enabled (`-Duserelocatableinc`).
Then the shebang lines of executable scripts point at
the installation time perl binary path.

So if you move your perl directory to other places,
the shebang lines of executable scripts point at a wrong perl binary and
we cannot execute scripts. Oops!

A solution of that problem is to replace shebang lines by

    #!/bin/sh
    exec "$(dirname "$0")"/perl -x "$0" "$@"
    #!perl

which means that scripts will be executed by the perl located in the same directory.

# SEE ALSO

- [Relocatable installations in perl5100delta.pod](https://metacpan.org/pod/distribution/perl/pod/perl5100delta.pod#Relocatable-installations)
- [https://github.com/shoichikaji/relocatable-perl](https://github.com/shoichikaji/relocatable-perl)
- [https://github.com/shoichikaji/relocatable-perl-growthforecast](https://github.com/shoichikaji/relocatable-perl-growthforecast)

# AUTHOR

Shoichi Kaji <skaji@cpan.org>

# COPYRIGHT AND LICENSE

Copyright 2018 Shoichi Kaji <skaji@cpan.org>

This library is free software; you can redistribute it and/or modify
it under the same terms as Perl itself.
