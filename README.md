# NAME

Test::Auto

# ABSTRACT

Test Automation, Docs Generation

# SYNOPSIS

    #!/usr/bin/env perl

    use Test::Auto;
    use Test::More;

    my $test = Test::Auto->new(
      't/Test_Auto.t'
    );

    # automation

    # my $subtests = $test->subtests->standard;

    # ...

    # done_testing;

# DESCRIPTION

This package aims to provide, a standard for documenting Perl 5 software
projects, a framework writing tests, and automation for validating the tests,
documentation, and usage examples.

# REASONING

This framework lets you write documentation in test files using pod-like
comment blocks. By using a particular set of comment blocks (the specification)
this framework can run certain kinds of tests automatically. For example, we
can automatically ensure that the package the test is associated with is
loadable, that the test file comment blocks meet the specification, that any
super-classes or libraries are loadable, and that the functions, methods, and
routines are properly documented.

# LIBRARIES

This package uses type constraints from:

[Data::Object::Library](https://metacpan.org/pod/Data::Object::Library)

# ATTRIBUTES

This package has the following attributes:

## data

    data(DataObject)

This attribute is read-only, accepts `(DataObject)` values, and is optional.

## file

    file(Str)

This attribute is read-only, accepts `(Str)` values, and is required.

# METHODS

This package implements the following methods:

## document

    document() : InstanceOf["Test::Auto::Document"]

This method returns a [Test::Auto::Document](https://metacpan.org/pod/Test::Auto::Document) object.

- document example #1

        # given: synopsis

        my $document = $test->document;

## parser

    parser() : InstanceOf["Test::Auto::Parser"]

This method returns a [Test::Auto::Parser](https://metacpan.org/pod/Test::Auto::Parser) object.

- parser example #1

        # given: synopsis

        my $parser = $test->parser;

## subtests

    subtests() : InstanceOf["Test::Auto::Subtests"]

This method returns a [Test::Auto::Subtests](https://metacpan.org/pod/Test::Auto::Subtests) object.

- subtests example #1

        # given: synopsis

        my $subtests = $test->subtests;

# SPECIFICATION

    # [required]

    =name
    =abstract
    =includes
    =synopsis
    =description

    # [optional]

    =libraries
    =inherits
    =integrates
    =attributes

    # [repeatable; optional]

    =method $name
    =signature $name
    =example-$number $name # [repeatable]

    # [repeatable; optional]

    =function $name
    =signature $name
    =example-$number $name # [repeatable]

    # [repeatable; optional]

    =routine $name
    =signature $name
    =example-$number $name # [repeatable]

The specification is designed to accommodate typical package declarations. It
is used by the parser to provide the content used in the test automation and
document generation.

## name

    =name

    Path::Find

    =cut

The `name` block should contain the package name. This is tested for
loadability.

## abstract

    =abstract

    Find Paths using Heuristics

    =cut

The `abstract` block should contain a subtitle describing the package. This is
tested for existence.

## includes

    =includes

    function: path
    method: children
    method: siblings
    method: new

    =cut

The `includes` block should contain a list of `function`, `method`, and/or
`routine` names in the format of `$type: $name`. Empty lines are ignored.
This is tested for existence. Each function, method, and/or routine is tested
to be documented properly. Also, the package must recognize that each exists.

## synopsis

    =synopsis

    use Path::Find 'path';

    my $path = path; # get path using cwd

    =cut

The `synopsis` block should contain the normative usage of the package. This
is tested for existence. This block should be written in a way that allows it
to be evaled successfully and should return a value.

## description

    =description

    interdum posuere lorem ipsum dolor sit amet consectetur adipiscing elit duis
    tristique sollicitudin nibh sit amet

    =cut

The `description` block should contain a thorough explanation of the purpose
of the package. This is tested for existence.

## libraries

    =libraries

    Types::Standard
    Types::TypeTiny

    =cut

The `libraries` block should contain a list of packages, each of which is
itself a [Type::Library](https://metacpan.org/pod/Type::Library). These packages are tested for loadability, and to
ensure they are type library classes.

## inherits

    =inherits

    Path::Tiny

    =cut

The `inherits` block should contain a list of parent packages. These packages
are tested for loadability.

## integrates

    =integrates

    Path::Find::Upable
    Path::Find::Downable

    =cut

The `integrates` block should contain a list of packages that are involved in
the behavior of the main package. These packages are not automatically tested.

## attributes

    =attributes

    cwd: ro, req, Object

    =cut

The `attributes` block should contain a list of package attributes in the form
of `$name: $is, $presence, $type`, where `$is` should be `ro` (read-only) or
`rw` (read-wire), and `$presence` should be `req` (required) or `opt`
(optional), and `$type` can be any valid [Type::Tiny](https://metacpan.org/pod/Type::Tiny) expression. Each
attribute declaration must be recognized to exist by the main package and have
a type which is recognized by one of the declared type libraries.

## methods

    =method children

    quis viverra nibh cras pulvinar mattis nunc sed blandit libero volutpat

    =signature children

    children() : [Object]

    =example-1 children

    # given: synopsis

    my $children = $path->children;

    =example-2 children

    # given: synopsis

    my $filtered = $path->children(qr/lib/);

    =cut

Describing a method requires at least three blocks, i.e. `method $name`,
`signature $name`, and `example-1 $name`. The `method` block should contain
a description of the method and its purpose. The `signature` block should
contain a method signature in the form of `$signature : $return_type`, where
`$signature` is a valid typed signature and `$return_type` is any valid
[Type::Tiny](https://metacpan.org/pod/Type::Tiny) expression. The `example-$number` block is a repeatable block,
and at least one block must exist when documenting a method. The
`example-$number` block should contain valid Perl code and return a value. The
block may contain a "magic" comment in the form of `given: synopsis` or
`given: example-$number $name` which if present will include the given code
example(s) with the evaluation of the current block. Each method is tested and
must be recognized to exist by the main package.

## functions

    =function path

    lectus quam id leo in vitae turpis massa sed elementum tempus egestas

    =signature children

    path() : Object

    =example-1 path

    package Test::Path::Find;

    use Path::Find;

    my $path = path;

    =cut

Describing a function requires at least three blocks, i.e. `function $name`,
`signature $name`, and `example-1 $name`. The `function` block should
contain a description of the function and its purpose. The `signature` block
should contain a function signature in the form of `$signature :
$return_type`, where `$signature` is a valid typed signature and
`$return_type` is any valid [Type::Tiny](https://metacpan.org/pod/Type::Tiny) expression. The `example-$number`
block is a repeatable block, and at least one block must exist when documenting
a function. The `example-$number` block should contain valid Perl code and
return a value. The block may contain a "magic" comment in the form of `given:
synopsis` or `given: example-$number $name` which if present will include the
given code example(s) with the evaluation of the current block. Each function
is tested and must be recognized to exist by the main package.

## routines

    =routine algorithms

    sed sed risus pretium quam vulputate dignissim suspendisse in est ante

    =signature algorithms

    algorithms() : Object

    =example-1 algorithms

    # given: synopsis

    $path->algorithms

    =example-2 algorithms

    package Test::Path::Find;

    use Path::Find;

    Path::Find->algorithms;

    =cut

Typically, a Perl subroutine is declared as a function or a method. Rarely, but
sometimes necessary, you will need to describe a subroutine where the invocant
is either a class or class instance. Describing a routine requires at least
three blocks, i.e. `routine $name`, `signature $name`, and `example-1
$name`. The `routine` block should contain a description of the routine and
its purpose. The `signature` block should contain a routine signature in the
form of `$signature : $return_type`, where `$signature` is a valid typed
signature and `$return_type` is any valid [Type::Tiny](https://metacpan.org/pod/Type::Tiny) expression. The
`example-$number` block is a repeatable block, and at least one block must
exist when documenting a routine. The `example-$number` block should contain
valid Perl code and return a value. The block may contain a "magic" comment in
the form of `given: synopsis` or `given: example-$number $name` which if
present will include the given code example(s) with the evaluation of the
current block. Each routine is tested and must be recognized to exist by the
main package.

# AUTOMATION

    $test->standard;

This is the equivalent of writing:

    $test->package;
    $test->document;
    $test->libraries;
    $test->inherits;
    $test->attributes;
    $test->methods;
    $test->routines;
    $test->functions;

This framework provides a set of automated subtests based on the package
specification, but not everything can be automated so it also provides you with
two powerful hooks into the framework for manual testing.

    my $subtests = $test->subtests;

    $subtests->synopsis(fun($tryable) {
      ok my $result = $tryable->result, 'result ok';

      $result; # for automated testing after the callback
    });

The code examples documented can be automatically evaluated (evaled) and
returned using a callback you provide for further testing. Because the code
examples are returned as [Data::Object::Try](https://metacpan.org/pod/Data::Object::Try) objects, this makes capturing and
testing exceptions simple, for example:

    my $subtests = $test->subtests;

    $subtests->synopsis(fun($tryable) {
      # synopsis throws an exception
      $tryable->catch('Path::Find::Error', sub {
        return $_[0];
      });
      ok my $result = $tryable->result, 'result ok';
      ok $result->isa('Path::Find::Error'), 'exception caught';

      $result;
    });

Finally, The other manual testing hook (with some automation) is the `example`
method. This hook evaluates (evals) a given example and returns the result as
a [Data::Object::Try](https://metacpan.org/pod/Data::Object::Try) object.

    my $subtests = $test->subtests;

    $subtests->example(-1, 'children', 'method', fun($tryable) {
      ok my $result = $tryable->result, 'result ok';

      $result;
    });

The test automation and document generation enabled through this framework
makes it easy to maintain source/test/documentation parity. This also
increases reusability and reduces the need for complicated state and test setup.

# AUTHOR

Al Newkirk, `awncorp@cpan.org`

# LICENSE

Copyright (C) 2011-2019, Al Newkirk, et al.

This is free software; you can redistribute it and/or modify it under the terms
of the The Apache License, Version 2.0, as elucidated in the
["license file"](https://github.com/iamalnewkirk/test-auto/blob/master/LICENSE).

# PROJECT

[Project](https://github.com/iamalnewkirk/test-auto)

[Milestones](https://github.com/iamalnewkirk/test-auto/milestones)

[Issues](https://github.com/iamalnewkirk/test-auto/issues)
