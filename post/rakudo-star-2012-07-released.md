%% title: Rakudo Star 2012.07 released
%% date: 2012-07-28

On behalf of the Rakudo and Perl 6 development teams, I'm happy to announce the July 2012 release of "Rakudo Star", a useful and usable distribution of Perl 6. The tarball for the July 2012 release is available from <a href="https://github.com/rakudo/star/downloads">https://github.com/rakudo/star/downloads</a>.

In the Perl 6 world, we make a distinction between the language ("Perl 6") and specific implementations of the language such as "Rakudo Perl". This Star release includes <a href="https://github.com/rakudo/rakudo/blob/master/docs/announce/2012.07">release 2012.07</a> of the <a href="http://github.com/rakudo/rakudo">Rakudo Perl 6 compiler</a>, version 4.6 of the <a href="http://parrot.org/">Parrot Virtual Machine</a>, and various modules, documentation, and other resources collected from the Perl 6 community.

Some of the new features added to this release include:

* Built-in metaobjects (e.g. Metamodel::ClassHOW) now inherit from Any

* &amp;open now supports the :enc/:encoding option

* anonymous subset types (e.g., 'subset :: of Int where { $_ &gt; 0 }')

* Rakudo Star now ships with the Template::Mojo module

This release also contains a range of bug fixes, improvements to error reporting and better failure modes. More exceptions are thrown as typed exceptions, and more meta-model errors have been fixed to properly report line numbers.

Starting with this release, we will also identify changes to the implementation or specification that can cause breakages in existing Perl 6 code. The following features have been deprecated or modified due to changes in the Perl 6 specification, and are being removed or changed as follows:

* IO::File and IO::Dir will go away, and &amp;dir now returns values of type IO::Path (which is currently the superclass of IO::File and IO::Dir). The return values of &amp;dir will still stringify to the base name of the returned file and directory names, and you can call .path on them to obtain the full path.

* Leading whitespace in rules and under :sigspace will no longer be converted to &lt;.ws&gt;. For existing regexes that expect this conversion, add a &lt;?&gt; in front of leading whitespace to make it meta again. Scheduled for the 2012.08 release.

* The ?-quantifier on captures in regexes currently binds the capture slot to a List containing either zero or one Match objects; i.e., it is equivalent to "** 0..1". In the future, the ?-quantifier will bind the slot directly to a captured Match or to Nil. Existing code
can manage the transition by changing existing ?-quantifiers to use "** 0..1", which will continue to return a List of matches. Scheduled for the 2012.08 release, but may end up in 2012.09 .

* The method Str.bytes will be removed. To get the number of codepoints in a string, use .codes instead. To get the number of bytes in a given encoding, use $str.encode($encoding).bytes . Scheduled for the 2012.08 release.

* The method Str.lcfirst will be removed without replacement. Scheduled for the 2012.08 release.

* The method Str.ucfirst will eventually be removed, and replaced by Str.tc. No schedule yet, depends on having tc implemented first.

* 'abs' is currently a prefix operator, and will be changed to a normal subroutine. Scheduled for the 2012.08 release.

* The integer argument to IO::Socket.recv will be interpreted as number of characters/codepoints. Scheduled for the 2012.08 release.

There are some key features of Perl 6 that Rakudo Star does not yet handle appropriately, although they will appear in upcoming releases. Some of the not-quite-there features include:

* macros
* threads and concurrency
* Unicode strings at levels other than codepoints
* interactive readline that understands Unicode
* non-blocking I/O
* much of Synopsis 9

There is a new online resource at <a href="http://perl6.org/compilers/features">http://perl6.org/compilers/features</a> that lists the known implemented and missing features of Rakudo Star 2012.07 and other Perl 6 implementations.

In many places we've tried to make Rakudo smart enough to inform the programmer that a given feature isn't implemented, but there are many that we've missed. Bug reports about missing and broken features are welcomed at.

See <a href="http://perl6.org/">http://perl6.org/</a> for links to much more information about Perl 6, including documentation, example code, tutorials, reference materials, specification documents, and other supporting resources. An updated draft of a Perl 6 book is available as &lt;docs/UsingPerl6-draft.pdf&gt; in the release tarball.

The development team thanks all of the contributors and sponsors for making Rakudo Star possible. If you would like to contribute, see <a href="http://rakudo.org/how-to-help">http://rakudo.org/how-to-help</a>, ask on the <a href="mailto:perl6-compiler@perl.org">perl6-compiler@perl.org</a> mailing list, or join us on IRC #perl6 on freenode.