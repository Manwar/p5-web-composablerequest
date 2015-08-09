# Name

Web::ComposableRequest - Composable request class for web frameworks

# Synopsis

    use Web::ComposableRequest;

    # List the roles to be applied to the request object base class
    my $config  = {
       prefix        => 'my_app',
       request_roles => [ 'L10N', 'Session', 'Cookie', 'JSON', 'Static' ], };

    # Construct a request object factory
    my $factory = Web::ComposableRequest->new( config => $config );

    # Request data provided by the web framework
    my $args    = 'arg1/arg2/arg_3';
    my $query   = { mid => '123_4' };
    my $cookie  = 'my_app_cookie1=key1%7Eval1%2Bkey2%7Eval2; '
                . 'my_app_cookie2=key3%7Eval3%2Bkey4%7Eval4';
    my $input   = '{ "key": "value_1" }';
    my $env     = { CONTENT_LENGTH  => 20,
                    CONTENT_TYPE    => 'application/json',
                    HTTP_COOKIE     => $cookie,
                    HTTP_HOST       => 'localhost:5000',
                    PATH_INFO       => '/Getting-Started',
                    'psgi.input'    => IO::String->new( $input ),
                    'psgix.session' => {},
                  };

    # Construct a new request object
    my $req     = $factory->new_from_simple_request( {}, $args, $query, $env );

# Description

Composes a request class from a base class plus a selection of applied roles

# Configuration and Environment

Defines the following attributes;

- `config`

    A configuration object created by passing the ["config\_attr"](#config_attr) to the constructor
    of the ["config\_class"](#config_class)

- `config_attr`

    Either a hash reference or an object reference or undefined. Overrides the
    hard coded configuration class defaults

- `config_class`

    A non empty simple string which is the name of the base configuration class

- `request_class`

    A non empty simple string which is the name of the base request class

# Subroutines/Methods

## `new_from_simple_request`

    my $req = $factory->new_from_simple_request( $opts, $args, $query, $env );

Returns a request object representing the passed parameters. The `$opts`
hash reference is used to directly set attributes in the request object.
The `$args` parameter is either a string of arguments after the path in the
URI or an upload object reference. The `$query` hash reference are the keys
and values of the URI query parameters, and the `$env` hash reference is the
Plack environment

# Diagnostics

None

# Dependencies

- [CGI::Simple](https://metacpan.org/pod/CGI::Simple)
- [Class::Inspector](https://metacpan.org/pod/Class::Inspector)
- [Exporter::Tiny](https://metacpan.org/pod/Exporter::Tiny)
- [HTTP::Body](https://metacpan.org/pod/HTTP::Body)
- [HTTP::Message](https://metacpan.org/pod/HTTP::Message)
- [JSON::MaybeXS](https://metacpan.org/pod/JSON::MaybeXS)
- [Moo](https://metacpan.org/pod/Moo)
- [Subclass::Of](https://metacpan.org/pod/Subclass::Of)
- [Try::Tiny](https://metacpan.org/pod/Try::Tiny)
- [URI](https://metacpan.org/pod/URI)
- [Unexpected](https://metacpan.org/pod/Unexpected)

# Incompatibilities

There are no known incompatibilities in this module

# Bugs and Limitations

There are no known bugs in this module. Please report problems to
http://rt.cpan.org/NoAuth/Bugs.html?Dist=Web-ComposableRequest.
Patches are welcome

# Acknowledgements

Larry Wall - For the Perl programming language

# Author

Peter Flanigan, `<pjfl@cpan.org>`

# License and Copyright

Copyright (c) 2015 Peter Flanigan. All rights reserved

This program is free software; you can redistribute it and/or modify it
under the same terms as Perl itself. See [perlartistic](https://metacpan.org/pod/perlartistic)

This program is distributed in the hope that it will be useful,
but WITHOUT WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE