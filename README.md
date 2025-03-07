# nanotest
Tiny testing toolkit (for Python)

For now at least, this repo is an archive of code I thought I had
lost forever, and was glad to discover in PyPi. I don't know how I
lost access to the code; I have other repos from around the same time
which survive to the present day, and I don't make it a habit to throw
away code. Oh well...

Nanotest was a tiny test harness for Python, that I wrote in 2012
and 2013. It's small both in terms of the actual code (which totals
335 SLOC), and in terms of what it tried to do. If my memory serves,
at that time Python testing was dominated by JUnit/XUnit style
frameworks which were very heavyweight and wanted lots of boilerplate
code. I wanted something light-feeling, on the model of Perl 5's
testing libraries that just let you test values using `assert` style
functions named things like `is` and `is_deeply`.

(Most people don't like testing. Why would you make it harder by
designing a testing library which is bulky and verbose? But I
digress.)

To make this work, I learned some pretty neat (and/or possibly
abusive) things about Python's internal compiler system -- and that's
the main reason I have found myself occasionally wishing that I could
find this code. Not because I want to use it for testing (at least, I
don't think I do... right now... probably), or because it was a beacon
of good design and code quality. But because it was a fun project that
taught me a lot and let me get a little weird with Python.

----

A lot of the work of getting this code into a shape I was happy with
happened over the 2012 holidays, on the farm of Sue Cassell McKinney,
near Lynchburg TN. Love you, Aunt Sue.
