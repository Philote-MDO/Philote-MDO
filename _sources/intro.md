![philote](graphics/logos/philote.svg)

# Introduction

Philote is a datastructure and communication standard for distributed
multidisciplinary design optimization (MDO) frameworks. It was developed
specifically for the Ansible MDO framework using protocol buffers and gRPC
to autogenerate code in a variety of languages. However, as it is merely a
datastructure and communication standard, it can be applied to a variety of MDO
frameworks. An example of this are the Computational System Domain Language
([CSDL](https://lsdolab.github.io/csdl/)) and [OpenMDAO](https://openmdao.org)
bindings, which enable those frameworks to call remote analysis disciplines.


## Motivation

As previously mentioned, Philote is a foundational piece of software written for
the Ansible MDO framework. Without going into more detail about this framework,
a central aspect it addresses is decentralized computing. Given that the
aforementioned CSDL and OpenMDAO frameworks exist (along with several commercial
offerings), it would be reasonable to ask why the world needs another MDO
framework. Well, mainly because the existing frameworks do not cover
decentralized computing (or commercial ones that do, do not offer robust
gradient-based capablilities).

Being decentralized requires some means of communication between the main
framework and the individual analysis disciplines. Moreover, the individual
disciplines may use a plethora of programming languages, some of which may not
easily wrap into Python, as required by both CSDL and OpenMDAO. Therefore,
Philote aims to define a standard for a server/client model for analysis
disciplines using [gRPC](https://grpc.io/). Using gRPC enables the
autogeneration of the required services and datastructures in a variety of
languages. Philote, however, does not provide implementation beyond the protocol
buffer ([protobuf](https://developers.google.com/protocol-buffers/))
definitions.

The definition of a data and communications standard allows Philote to be used
beyond the Ansible MDO tool. The absence of implementation beyond the
auto-generated code allows for flexibility of use. However, the goal is to
provide enough of an auto-generated template for analysis tool developers to
easily implement MDO disciplines and couple them into a large variety of
frameworks using the same communication mechanism. A number of examples are in
the works to ease the development process of analysis discipline servers.


## Origin of the Project Name

Inevitably, people ask about the origin of project names, especially if they
aren't obviously discernable. The name "Philote" was chosen because of its
relationship to the ansible network in Orson Scott Card's Ender novels (Ender's
Game, Speaker for the Dead, etc.). In the series, Philotes are the most
elementary building block in the universe and are used to enable faster than
light communications via the ansible network.


## License Overview and Philosophy

Licensing is an important topic in software, especially for tools that are meant
to be used within larger frameworks. Because licensing can be a reason for or
against using a piece of software, this section provides a brief overview of the
license governing the use of Philote and why this particular license was chosen.
In addition, there is a separate chapter on licensing.

Philote is licensed under the Apache version 2 open-source license.

<!-- :::{sidebar} My sidebar title
My sidebar content
::: -->