# asn1go

## Rationale

Currently existing Go libraries for asn1 support are either reflection-based (crypto/asn1) or 
very low-level (golang.org/x/crypto/cryptobyte). Idea is to provide Protobuf-like experience for 
working with ASN1 in Golang.

Originally started to back [gorberos](https://github.com/chemikadze/gorberos) kerberos wannabe-library.

## Architecture

1) Custom Lexer consumes from bufio.Reader and called by Parser
2) Parser is built using [goyacc](https://godoc.org/golang.org/x/tools/cmd/goyacc)
 based on BNF provided in [X.680](https://www.itu.int/ITU-T/studygroups/com17/languages/X.680-0207.pdf) standard. 
 As the result, Parser produces ASN1 module AST.
3) AST is used by Code Generator to produce declarations, serialization, and deserialization code.

## Roadmap

1) Lexer
 - [x] identifiers
 - [x] numbers 
 - [x] keywords
 - [x] symbols
 - [ ] strings, bit strings, hex strings
 - [ ] XML
2) Parser
 - [x] minimal module definition BNF
 - [x] complete BNF to consume Kerberos module
 - [x] yield AST from parser
 - [x] parse SNMPv1 (rfc1157, rfc1155)
 - [ ] parse LDAP (rfc4511) 
 - [ ] SNMPv2 (rfc3411–3418)
3) Code Generator
 - [ ] declaration generator
 - [ ] crypto/asn1 compatible generation mode
 - [ ] DER serialization generator
 - [ ] DER deserialization generator
 