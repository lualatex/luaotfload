=======================================================================
                            luaotfload-tool
=======================================================================

-----------------------------------------------------------------------
         generate and query the Luaotfload font names database
-----------------------------------------------------------------------

:Date:      2013-06-02
:Copyright: GPL v2.0
:Version:   2.3
:Manual section: 1
:Manual group: text processing

SYNOPSIS
=======================================================================

**luaotfload** [ -bDcfFipquvVh ]

**luaotfload** --update [ --force ] [ --quiet ] [ --verbose ] [ --prefer-texmf ] [ --dry-run ]

**luaotfload** --find=FONTNAME [ --fuzzy ] [ --info ]

**luaotfload** --flush-lookups

**luaotfload** --cache=DIRECTIVE

**luaotfload** --list=CRITERION[:VALUE] [ --fields=F1,F2,...,Fn ]

**luaotfload** --help

**luaotfload** --version

**luaotfload** --show-blacklist

DESCRIPTION
=======================================================================

luaotfload-tool accesses the font names database that is required by
the *Luaotfload* package. There are two general modes: **update** and
**query**.

+ **update**:  update the database or rebuild it entirely;
+ **query**:   resolve a font name or display close matches.

A third mode for clearing the lookup cache is currently experimental.

Note that if the script is named ``mkluatexfontdb`` it will behave like
earlier versions (<=1.3) and always update the database first. Also,
the verbosity level will be set to 2.

OPTIONS
=======================================================================

update mode
-----------------------------------------------------------------------
--update, -u            Update the database; indexes new fonts.
--force, -f             Force rebuilding of the database; re-indexes
                        all fonts.
--prefer-texmf, -p      Organize the file name database in a way so
                        that it prefer fonts in the *TEXMF* tree over
                        system fonts if they are installed in both.
--dry-run, -D           Don’t load fonts, scan directories only.
                        (For debugging file system related issues.)

query mode
-----------------------------------------------------------------------
--find=NAME             Resolve a font name; this looks up <name> in
                        the database and prints the file name it is
                        mapped to.
--fuzzy, -F             Show approximate matches to the file name if
                        the lookup was unsuccessful (requires
                        ``--find``).
--info, -i              Display basic information to a resolved font
                        file (requires ``--find``).
--show-blacklist, -b    Show blacklisted files (not directories).
--list=CRITERION        Show entries, where *CRITERION* is one of the
                        following:

                        1) the character ``*``, selecting all entries;
                        2) a field of a database entry, for instance
                           *fullname* or *units_per_em*, according to
                           which the output will be sorted; or
                        3) an expression of the form ``field:value`` to
                           limit the output to entries whose ``field``
                           matches ``value``.

--fields=FIELDS         Comma-separated list of fields that should be
                        printed.  The default is *fullname,version*.
                        (Only meaningful with ``--list``.)

font and lookup caches
-----------------------------------------------------------------------
--flush-lookups         Clear font name lookup cache (experimental).

--cache=DIRECTIVE       Cache control, where *DIRECTIVE* is one of the
                        following:

                        1) ``purge`` -> delete Lua files from cache;
                        2) ``erase`` -> delete Lua and Luc files from
                           cache;
                        3) ``show``  -> print stats.

miscellaneous
-----------------------------------------------------------------------
--verbose=N, -v         Set verbosity level to *n* or the number of
                        repetitions of ``-v``.
--quiet                 No verbose output (log level set to zero).
--log=stdout            Redirect log output to terminal (for database
                        troubleshooting).

--version, -V           Show version number and exit.
--help, -h              Show help message and exit.


FILES
=======================================================================

The font name database is usually located in the directory
``texmf-var/luatex-cache/generic/names/`` (``$TEXMFCACHE`` as set in
``texmf.cnf``) of your *TeX Live* distribution as
``luaotfload-names.lua``.  The experimental lookup cache will be
created as ``luaotfload-lookup-cache.lua`` in the same directory.
Both files are safe to delete, at the cost of regenerating them with
the next run of *LuaTeX*.

SEE ALSO
=======================================================================

**luatex** (1), **lua** (1)

* ``texdoc luaotfload`` to display the manual for the *Luaotfload*
  package
* Luaotfload development `<https://github.com/lualatex/luaotfload>`_
* LuaLaTeX mailing list  `<http://tug.org/pipermail/lualatex-dev/>`_
* LuaTeX                 `<http://luatex.org/>`_
* ConTeXt                `<http://wiki.contextgarden.net>`_
* Luaotfload on CTAN     `<http://ctan.org/pkg/luaotfload>`_

BUGS
=======================================================================

Tons, probably.

AUTHORS
=======================================================================

*Luaotfload* is maintained by the LuaLaTeX dev team
(`<https://github.com/lualatex/>`__).
The fontloader code is provided by Hans Hagen of Pragma ADE, Hasselt
NL (`<http://pragma-ade.com/>`__).

This manual page was written by Philipp Gesang
<philipp.gesang@alumni.uni-heidelberg.de>.

