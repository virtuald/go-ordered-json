nspcc-dev fork of go-ordered-json
===============

There are some legacy/stupid applications[1] that you need to interoperate with,
and they for whatever reason require that the JSON you're using is ordered in
a particular way (contrary to the JSON specifications).

Unfortunately, the golang authors are not willing to support such a broken use
case, so on [their advice](https://groups.google.com/forum/#!topic/golang-dev/zBQwhm3VfvU)
this is a fork of the golang encoding/json package, with the ordered JSON
support originating with a patch from
[Peter Waldschmidt](https://go-review.googlesource.com/c/7930/).

**If you can, you should avoid using this package**. However, if you can't
avoid it, then you are welcome to. Provided under the MIT license, just like
golang.

Known broken applications 
-------------------------

* [1][Windows Communication Foundation Json __type ordering](https://docs.microsoft.com/en-us/dotnet/framework/wcf/feature-details/stand-alone-json-serialization#type-hint-position-in-json-objects)
* [2][NEO node](https://github.com/neo-project/neo/tree/master/src/neo/IO/Json)

Fork motivations
-------------------------

NEO project has its own implementation of JSON serializer which is more a JSON
dialect rather than standard-compatible implementation. Until JSON serialisation
format affects contract states we need to be byte-to-byte compatible with the
reference JSON serializer. This fork contains the following compatibility quirks:

* JSON serializer is ordered (see https://github.com/nspcc-dev/neo-go/pull/2026)
* JSON serializer escapes non-ascii characters while marshalling (see https://github.com/nspcc-dev/neo-go/pull/2174)

More compatibility quirks may be added in the future.