# Data Representation

This section describes the data conventions provided by Philote.


## Array Types

message DoubleArray {
    // array shape
    repeated int64 index = 1;

    // continuous data
    repeated double data = 2;
}


message IntArray {
    // array shape
    repeated int64 index = 1;

    // continuous data
    repeated int64 data = 2;
}


## Variable Data

message Variables {
    // continuous data
    map <string, DoubleArray> continuous = 1;

    // discrete data
    map <string, IntArray> discrete = 2;
}


## Variable Meta Data

message VariableMetaData {
    // variable name
    string name = 1;

    // variable shape
    repeated int64 id = 2;

    // variable units
    string units = 3;
}


## Partials Data

Pair:

    message Pair {
        // name of the function
        string f = 1;

        // name of the variable
        string x = 2;
    }


Partials:


    message Partials {
        // map of all partials arrays
        map <Pair, DoubleArray> data = 1;
    }


## Chunk Datatype

message Chunk {
    bytes data = 1;
}