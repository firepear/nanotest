# nanotest
Tiny testing toolkit (for Python)

For now this repo is not _archived_ (in GitHub terms), but it should
be treated _as an archive._ This is decade+ old code which I thought I
had lost forever, and was glad to discover in PyPi. If you actually
want to write tests for Python code, you want to go look at
[pytest](https://pytest.org/).

----

I don't know how I lost access to the code; I have other repos from
around the same time which survive to the present day, and I don't
make it a habit to throw away code. Oh well...

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


## Code archaeology

I haven't seen this code since early 2013. Let's go on a little dive, shall we?

### 07 Mar 2025

The very first thing I discovered was that the runner is not runnable,
because I gave it a a shebang of `#!/usr/bin/env python`. I had
already moved to Python 3 at this time, but I was also using Arch
Linux, whose stance at the time was "everyone should move to Python 3,
and that's now `python` on our systems; if you want _old python_ you
can find it over at `python2`".

These days it seems that people have mostly settled on just having
`python3` and `python2`. So after making that change...

```
$ ./bin/nanotest-py
No tests found; nothing to do.
```

Uh huh. My testing library has no tests. That feels like a bad look --
though I have a ghost of a memory that due to my (ab)use of
`compile()` and poking directly at live compiled code representation,
testing the internal functions of this library would have been a
sketchy proposition.

Anyway, how was I supposed to use this thing?

```
$ ./bin/nanotest-py -h
usage: nanotest-py [-h] [-j] [-s] [-n] [-v] [-d] [TEST ...]

Find any and all files matching '*/tests/*py' in the current directory tree, and run them as nanotest-py tests.

positional arguments:
  TEST             Execute specified test files instead of searching tree

options:
  -h, --help       show this help message and exit
  -j, --json       Dump all test results to STDOUT as JSON (disables other output; result will be an empty list if no tests are found)
  -s, --silent     Output nothing at all, indicating test failure by return code (0: success, 1: failure, 2: no tests found)
  -n, --noprepend  Do not prepend the current directory to sys.path; append instead
  -v, --version    Display version numbers
  -d, --dev        Run developer tests also
```

Okay, right off the bat I have some questions and notes for 2013 me:

- `nanotest-py`, huh? Planning to port this to other languages, were
  we? Hubris much?
- Why did I list all the options individually in the compact usage
  example?
  - Edit: I didn't; `argparse` did. Whew.
- The JSON argument was initially confusing, but I think I remembered
  why I added that. I'll get to it later.
- The `silent` arg is pointless; if you want your test results to be
  quiet, you can redirect them
  - This is a good example of something I've been fighting against
    since my very first software project: the urge to just handle too
    many cases/eventualities. Initially it was driven by trying to be
    clever, but I've done _a lot_ of work on that and these days it's
    mostly attempts to _be helpful_ and do things for users. But that
    frequently stands in opposition to the [Unix
    philosophy](https://en.wikipedia.org/wiki/Unix_philosophy).
- I legitimately have no memory of the `noprepend` thing. I assume the
  code will enlighten me when I get into it
- What the hell is a "developer test"? Are all tests not developer
  tests? Sure, a user _can_ run tests when they have source, but does
  anyone, ever? Again, I think I'm gonna need the code to explain
  myself to me here

Sidebar: About the `json` arg: this one is hazy as well, but I _think_
I had an idea about defining a structured data format for modern CLI
tools, to make screen-scraping a thing of the past. And honestly,
that's still a neat idea, but whooo that's a tall order. Both on the
definition side and on the getting people to implement it side. I
can't remember the name that I had given this concept in my
head... I'm remembering Standard Tool Interchange Format, but that's
STIF (lol), and I'm simultaneously remembering that it shortened down
to SCIF? Anyhow, I think that's what JSON output was for here.

More to come soon...
