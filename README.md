# wets-s

`wets-s` is a WETS service that interacts with a
[nats-server](https://nats.io/)
to allow WETS simulators written in any language that supports NATS.

This is a literate programming document that requires additional tooling
to create the code and documentation present in this project. It is written in
[Asciidoctor](https://docs.asciidoctor.org/) and requires the
[atangle](https://repos.modelrealization.com/cgi-bin/fossil/mrtools/wiki?name=Aweb+Downloads)
tool to un-tangle the source code.

## Necessities

`wets-s.tcl` wraps the WETS model translation with a NATS client available
from <https://github.com/kazmirchuk/nats-tcl>. I made this into a module and
put it into the same place that I put the `Rosea` and `tclral` modules.

A nats-server must be configured and running. This is available from
https://nats.io/download/.

`wdriver.tcl`, the test driver included in the literate program document, uses
the `nats-tcl` client, connects to the server and starts a vessel into the
WETS model via `wets-s.tcl`.
