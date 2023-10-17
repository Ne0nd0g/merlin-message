# merlin-message

Messages and embedded Jobs exchanged between a Merlin Server and a Merlin Agent.

This package was separated out so that it can be updated independently of the Merlin Server and Agent packages.

Gob-encoded messages must come from the same package for the encoding and decoding to work between the Server and Agent.
Merlin Agent traffic can use gob encoding, but it is not required to. Encoding transforms must match how the Merlin 
Server listener is configured.
