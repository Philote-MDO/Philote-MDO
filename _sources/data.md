# Data Representation

This section describes the data conventions provided by Philote.



## Array Types

Philote provides two different types of arrays: one for continuous and the other
for discrete data. Any variable that gradients are required for must be defined
as continous data. The datatype for continuous data is the ``DoubleArray``:

    message DoubleArray {
        // array shape
        repeated int64 index = 1;

        // continuous data
        repeated double data = 2;
    }

It describes an n-dimensional array by providing the array shape as a list of
integers. The array data is saved as a single dimensional array (serialized) of
double precision values.

:::{note}
By convention, Philote arrays are described in ``row major`` order.
:::

Similarly, discrete data is defined as array of integers (``IntArray``). While
discrete data in an MDO problem can generally take any form or datatype, this
generality would add unnecessary complexity to Philote's design. Integer's
account for the vast majority of cases of discrete variables. As such, Philote
limits its representation of discrete data to integer arrays:

    message IntArray {
        // array shape
        repeated int64 shape = 1;

        // continuous data
        repeated int64 data = 2;
    }

Again, analogous to the double array, the implementation is that of an
n-dimensional array described by a shape array and an integer (64-bit) array
containing the serialized variable data (row major).


## Variable Data

While the array representations are necessary to describe data, arrays are not
sent over the wire directly. Instead a variable datatype is defined which
component function calls can pass to and from the analysis servers. The
``Variables`` datatype combines the array datatypes with a string key value to
enable decoding the variable by name:

    message Variables {
        // continuous data
        map <string, DoubleArray> continuous = 1;

        // discrete data
        map <string, IntArray> discrete = 2;
    }

While the ``Variables`` datatype contains both continuous and discrete data, it
should be noted that both fields should be treated as optional. This enables
sending either data types independently or together. There are cases, however,
where discrete data may not be included for an analysis. Variables datatypes are
both used for function inputs as well as function return values (discrete
outputs may also be provided).


## Variable Meta Data

In addition to variable analysis data, meta data is needed for many MDO
frameworks to define variable dimensions/shape as well as identify variable
units. Philote defines a datatype to describe required meta data,
``VariableMetaData``:

    message VariableMetaData {
        // flag to identify the variable as an input
        bool input = 1;

        // variable name
        string name = 2;

        // variable shape
        repeated int64 id = 3;

        // variable units
        string units = 4;
    }

This includes the variable name, the shape/dimensions of the variable, and
variable units as a string (units must be consistent across an n-dimensional
variable). This datatype is sent to the framework during the setup phase and
enables the MDO framework to define and allocate the inputs and outputs. Note
the bool flag that denotes if the variable is an input or output (true denotes
an input).


## Derivative (Partials) Data

Derivative information is not passed using the Variables datatype. Instead a
separate datatype, ``Partials``, is defined to pass derivative data over the
wire:

    message Partials {
        // map of all partials arrays
        map <Pair, DoubleArray> data = 1;
    }

One reason for the different datatype is that a derivative is defined by two
identifiers: the function as well as the variable it is differentiated by. To
identify these, a helper datatype, ``Pair``, is used:

    message Pair {
        // name of the function
        string f = 1;

        // name of the variable
        string x = 2;
    }

Otherwise, the Partials type is similar to the Variables type, except that no
discrete array is provided (as no gradients can be obtained from discrete data).


## Chunk Datatype

Finally, a ``Chunk`` datatype is defined to allow sending large datasets:

    message Chunk {
        bytes data = 1;
    }

gRPC limits message sizes to 4MB. Due to this limitation, and because MDO data
sizes can be considerably larger, there is a need to chunk the data that is sent
for every remote procedure call, stream it over the wire, and reassemble it at
the other end.