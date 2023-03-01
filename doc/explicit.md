# Explicit Components

The previous section described how data is represented by Philote. Individual
disciplines are described as a service. This section describes the conventions
for the ``ExplicitComponent``:

    service ExplicitComponent {
        // Sets up the component
        rpc Setup (google.protobuf.Empty) returns (Stream VariableMetaData) {}

        // Calls the component Compute function
        rpc Compute (Stream Chunk) returns (Stream Chunk) {}

        // Calls the component ComputePartials function
        rpc ComputePartials (stream Chunk) returns (stream Chunk) {}
    }


## Setup

The setup remote procedure call (``RPC``) enables the MDO framework to query the
analysis server for information about inputs and outputs. Frameworks, such as
OpenMDAO, may use this to allocate the variable and define units. However, in
general, this RPC is optional (for the MDO framework). It should still be
implemented by the analysis server, to avoid compatibility issues when switching
between MDO frameworks.


## Compute

The most basic RPC required by an MDO framework is a function evaluation. The
Compute RPC sends the input variables (``Variables``,chunked) to the analysis
server. The server then conducts a function evaluation and assigns output data
to a Variables datatype, chunks it, and streams the chunks back over the wire to
the MDO framework.


## Compute Partials

This RPC enables the MDO framework to query the discipline derivatives.
Naturally, not all disciplines are differentiable or meant to be used in
gradient-based optimization. As such, this function is optional.

Inputs are sent to the analysis server as a stream of chunks containing a
Variables datatype. After the analysis server has evaluated and assigned the
derivatives, the are returned (chunked) as a Partials datatypes.
