# cl-pinner -  Pinnable Common Lisp packages from any version control system endpoint

Have you ever wanted to run multiple versions of the *same* packages?
Well, now you can!

## Disclaimer
NOTE: This is still alpha quality and in the prototypal stages.

Please DO NOT use for any type of production system!

# Usage
## Loading an external system pinned to a specific version
To pull in the Ahungry Fleece package (a dependency of this project
that isn't on Quicklisp until next month), you can run in your REPL
(after cloning and loading this project):

```lisp
(fetch-and-load
  "git" "ahungry-fleece"
  "https://github.com/ahungry/ahungry-fleece" "master")
```

This will load it up with the master branch checked out, and the
package will then be loaded up automatically as:

```lisp
(ql:quickoad :vmaster.ahungry-fleece)
```

You can then try out an earlier version of the same repository, by
doing:

```lisp
(fetch-and-load
  "git" "ahungry-fleece"
  "https://github.com/ahungry/ahungry-fleece" "0.3.1")
```

This will load it up with the 0.3.1 tag checked out, and the
package will then be loaded up automatically as:

```lisp
(ql:quickoad :v0.3.1.ahungry-fleece)
```

with sub-dependencies identified as `v0.3.1.af.lib.io` etc.

and yes, you *CAN* run both at the same time in the same Common Lisp
REPL/image without any conflicts! (just make sure you import-from or
use-package the version as needed, or make the fully qualified
function calls).


# Running the tests (todo)
Tests for this repo are to come soon.

## CLI
Build with `cat build.sh | sh` in the project root.

Then you can use a simple `make test` in the future to test changes.

## REPL
To run tests in the REPL: `(ql:quickload :cl-pinner) (cl-pinner.run.tests:main)`

# TODO

* Need to support fetchers other than git (and VC systems such as mercurial/svn).
* Need to add the unit tests
* Need to add CLI / roswell style commands
* Need to add YAML style configuration loading/parsing

## Upcoming YAML configuration systems

You can see a sample of the planned out yaml configuration loader that
this system will work with here (or in the repo pinned.yml file):

```yml
# Define some dependencies
system:
  # A great utility library
  ahungry-fleece:
    type: git
    uri: https://github.com/ahungry/ahungry-fleece.git
    version: 0.3.1

```

This will allow the user an easy location to specify the exact
versions of each library they want the sytsem to fetch and load,
without having to modify their own project's ASDF file all the time.

## License
GPLv3
