# Rails Class Renamer

Rename a class in a Rails project. This will rename the corresponding source code and spec files, and search and replace the class name in your code.

Word boundaries are honoured, so renaming the class "Foo" should not affect the class "FooBar".

## INSTALLATION

Put the file "rename_class" somewhere on your PATH and make it executable.

## USAGE

    rename_class Foo Bar

NB: The script should be invoked from the root directory of a rails project.

## ASSUMPTIONS/PRE-REQUISITES

* Requires ActiveSupport (for CamelCase <-> snake_case conversions)
* Assumes that class FooBar is in a file (somewhere) called foo_bar.rb
* Assumes that *all* files called foo_bar.rb should be renamed if class FooBar is renamed
* Only works on Unixy systems with sensible implmentations of 'find', 'grep' and 'sed' (it works on a Mac).

## CAVEATS

I *strongly* recommend that you start from a clean git checkpoint, whenever you use this tool, so that you can easily roll back any changes with; "git checkout . ; git clean -f"

* Namespaced class names (e.g. renaming Foo::Bar to Baz::Zog) are not supported (yet).
* If your old class name occurs in a string literal, it will be renamed there, too. This may not be what you want.
* If you have a namespace that matches your old class name (e.g. you have a class "Foo::Bar::Baz" and you rename "Bar" to "Wibble"), the namespace will be renamed in your code (to Foo::Wibble::Baz) but the corresponding directory will not be renamed, so stuff will break.
